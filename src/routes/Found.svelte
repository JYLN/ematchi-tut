<script lang="ts">
	import { getTwemoji } from './utils';

	export let foundPairs: string[];
</script>

<div class="found">
	{#each foundPairs as emoji (emoji)}
		<img alt={emoji} src={getTwemoji(emoji)} />
	{/each}
</div>

<style>
	.found {
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 0.5em;
	}

	img {
		height: 5em;
		width: 5em;
	}
</style>
