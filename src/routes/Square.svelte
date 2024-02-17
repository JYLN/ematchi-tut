<script lang="ts">
	import { send } from './transitions';
	import { getTwemoji } from './utils';

	export let emoji: string;
	export let selected: boolean;
	export let found: boolean;
	export let group: 'a' | 'b';
</script>

<div class="square" class:flipped={selected || found}>
	<button on:click />

	<div class="background" />

	{#if !found}
		<img out:send={{ key: `${emoji}:${group}` }} alt={emoji} src={getTwemoji(emoji)} />
	{/if}
</div>

<style>
	.square {
		display: flex;
		justify-content: center;
		align-items: center;
		transform-style: preserve-3d;
		transition: transform 0.5s;
	}

	.flipped {
		transform: rotateY(180deg);
	}

	button {
		position: absolute;
		width: 100%;
		height: 100%;
		cursor: pointer;
		backface-visibility: hidden;
		background: #eee;
		border: none;
		border-radius: 1em;
		font-size: inherit;
	}

	.background {
		background-color: white;
		border: 0.2em solid #eee;
		position: absolute;
		transform: rotateY(180deg);
		backface-visibility: hidden;
		width: 100%;
		height: 100%;
		border-radius: 1em;
	}

	img {
		width: 6em;
		height: 6em;
		pointer-events: none;
		transform: rotateY(180deg);
		backface-visibility: hidden;
	}
</style>
