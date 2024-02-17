<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	import Square from './Square.svelte';

	export let grid: string[];
	export let foundPairs: string[];

	const dispatch = createEventDispatcher();

	let a = -1;
	let b = -1;
	let resetTimeout: number;
</script>

<div class="grid">
	{#each grid as emoji, i}
		<Square
			{emoji}
			on:click={() => {
				clearTimeout(resetTimeout);
				// If not selected
				if (a === -1 && b === -1) {
					a = i;
				} else if (b === -1) {
					b = i;
					if (grid[a] === grid[b]) {
						//correct pair
						dispatch('found', {
							emoji
						});
					} else {
						//incorrect pair
						resetTimeout = setTimeout(() => {
							a = b = -1;
						}, 1000);
					}
				} else {
					b = -1;
					a = i;
				}
			}}
			selected={i === a || i === b}
			found={foundPairs.includes(emoji)}
		/>
	{/each}
</div>

<style>
	.grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-template-rows: repeat(4, 1fr);
		height: 100%;
		gap: 0.5em;
		perspective: 100vw;
	}
</style>
