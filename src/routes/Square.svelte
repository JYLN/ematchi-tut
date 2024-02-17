<script lang="ts">
	import { getTwemoji } from './utils';

	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
</script>

<div class="square" class:flipped={selected}>
	<button on:click />

	{#if !found}
		<img alt={emoji} src={getTwemoji(emoji)} />
	{/if}
</div>

<style>
	.square {
		background-color: yellow;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.flipped button {
		background-color: red;
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
		cursor: pointer;
	}

	img {
		width: 6em;
		height: 6em;
		pointer-events: none;
	}
</style>
