<script lang="ts">
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

<style>
	h1 {
		font-size: 4em;
	}

	h1 span {
		color: purple;
	}

	p {
		font-family: Grandstander;
	}
</style>
