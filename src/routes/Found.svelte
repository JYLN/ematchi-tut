<script lang="ts">
	import { receive } from './transitions';
	import { getTwemoji } from './utils';

	export let foundPairs: string[];
</script>

<div class="found">
	{#each foundPairs as emoji (emoji)}
		<div class="pair">
			<img in:receive={{ key: `${emoji}:a` }} alt={emoji} src={getTwemoji(emoji)} />
			<img in:receive={{ key: `${emoji}:b` }} alt={emoji} src={getTwemoji(emoji)} />
		</div>
	{/each}
</div>

<style>
	.found {
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
		filter: drop-shadow(0.2em 0.2em 0.5em rgba(0, 0, 0, 0.5));
	}

	.pair {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 4em;
		height: 4em;
		background-color: white;
		padding: 1em;
		border-radius: 50%;
	}

	img {
		position: absolute;
		width: 2em;
		height: 2em;
	}
</style>
