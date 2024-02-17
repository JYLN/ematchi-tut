<script lang="ts">
	import Grid from './Grid.svelte';
	import { levels, type Level } from './levels';
	import { shuffle } from './utils';

	const level = levels[0];

	let size: number = level.size;
	let grid: string[] = createGrid(level);
	let foundPairs: string[] = [];

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
</script>

<div class="game">
	<div class="info"></div>

	<div class="grid-container">
		<Grid
			{grid}
			on:found={(e) => {
				foundPairs = [...foundPairs, e.detail.emoji];
			}}
			{foundPairs}
		/>
	</div>

	<div class="info"></div>
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
		background-color: purple;
	}

	.grid-container {
		width: 80em;
		height: 80em;
		background-color: aqua;
	}
</style>
