<script lang="ts">
	import { confetti } from '@neoconfetti/svelte';
	import '../styles.css';
	import Game from './Game.svelte';
	import Modal from './Modal.svelte';
	import { levels } from './levels';

	let state: 'waiting' | 'playing' | 'paused' | 'win' | 'lose' = 'waiting';
	let game: Game;
</script>

<Game
	bind:this={game}
	on:play={() => (state = 'playing')}
	on:pause={() => (state = 'paused')}
	on:win={() => (state = 'win')}
	on:lose={() => (state = 'lose')}
/>

{#if state !== 'playing'}
	<Modal>
		<header>
			<h1>e<span>match</span>i</h1>
			<p>the emoji matching game</p>
		</header>

		{#if state === 'win' || state === 'lose'}
			<p>you {state} the game!</p>
		{:else if state === 'paused'}
			<p>paused</p>
		{:else if state === 'waiting'}
			<p>Choose a level</p>
		{/if}

		<div class="button-container">
			{#if state === 'paused'}
				<button>resume</button>
				<button>quit</button>
			{:else}
				{#each levels as level}
					<button
						on:click={() => {
							game.start(level);
						}}
					>
						{level.label}
					</button>
				{/each}
			{/if}
		</div>
	</Modal>
{/if}

{#if state === 'win'}
	<div class="confetti" use:confetti={{ stageHeight: innerHeight, stageWidth: innerWidth }} />
{/if}

<style>
	h1 {
		font-size: 4em;
		margin-bottom: 0.1em;
	}

	h1 span {
		color: purple;
	}

	p {
		font-family: Grandstander;
	}

	.button-container {
		margin-top: 2em;
		display: flex;
		justify-content: center;
		align-content: center;
		gap: 1em;
	}

	.button-container button {
		background-color: purple;
		border: none;
		padding: 1em 1.75em;
		color: white;
		border-radius: 1em;
		cursor: pointer;
	}

	.confetti {
		position: fixed;
		width: 100%;
		height: 100%;
		top: 30%;
		left: 50%;
		pointer-events: none;
	}
</style>
