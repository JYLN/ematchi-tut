<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import Countdown from './Countdown.svelte';
	import Found from './Found.svelte';
	import Grid from './Grid.svelte';
	import { type Level } from './levels';
	import { shuffle } from './utils';

	const dispatch = createEventDispatcher();

	let size: number;
	let grid: string[] = [];
	let foundPairs: string[] = [];
	let remaining: number = 0;
	let duration: number = 0;
	let playing: boolean = false;

	export function start(level: Level) {
		size = level.size;
		grid = createGrid(level);
		remaining = duration = level.duration;
		foundPairs = [];

		resume();
	}

	function resume() {
		playing = true;
		countdown();

		dispatch('play');
	}

	function createGrid(level: Level) {
		const copy = [...level.emojis];
		const pairs: string[] = [];

		for (let i = 0; i < level.size ** 2 / 2; i++) {
			const index = ~~(Math.random() * copy.length);
			const emoji = copy[index];

			copy.splice(index, 1);
			pairs.push(emoji);
		}

		pairs.push(...pairs);
		return shuffle(pairs);
	}

	function countdown() {
		const start = Date.now();
		let remainingAtStart = remaining;

		function loop() {
			if (!playing) return;

			requestAnimationFrame(loop);

			remaining = remainingAtStart - (Date.now() - start);

			if (remaining <= 0) {
				dispatch('lose');
				playing = false;
				foundPairs = [];
			}
		}

		loop();
	}
</script>

<div class="game" style="--size: {size}">
	<div class="info">
		{#if playing}
			<Countdown
				{remaining}
				{duration}
				on:click={() => {
					dispatch('pause');
					playing = false;
				}}
			/>
		{/if}
	</div>

	<div class="grid-container">
		<Grid
			{grid}
			on:found={(e) => {
				foundPairs = [...foundPairs, e.detail.emoji];

				if (foundPairs.length === (size * size) / 2) {
					dispatch('win');
					playing = false;
				}
			}}
			{foundPairs}
		/>
	</div>

	<div class="info">
		<Found {foundPairs} />
	</div>
</div>

<style>
	.game {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100%;
		font-size: min(1vmin, 0.4rem);
	}

	.info {
		width: 80em;
		height: 10em;
	}

	.grid-container {
		width: 80em;
		height: 80em;
	}
</style>
