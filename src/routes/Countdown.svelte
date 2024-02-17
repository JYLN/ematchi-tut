<script lang="ts">
	export let remaining: number;
	export let duration: number;
</script>

<div class="countdown">
	<button>
		<svg
			xmlns="http://www.w3.org/2000/svg"
			width="24"
			height="24"
			viewBox="0 0 24 24"
			fill="#CCC"
			stroke="#999"
			stroke-width="2"
			stroke-linecap="round"
			stroke-linejoin="round"
			class="lucide lucide-pause-circle"
		>
			<circle cx="12" cy="12" r="10" /><line x1="10" x2="10" y1="15" y2="9" /><line
				x1="14"
				x2="14"
				y1="15"
				y2="9"
			/>
		</svg>
	</button>

	<div class="duration">
		<div class="remaining" style="--p: {remaining / duration}"></div>
	</div>
</div>

<style>
	.countdown {
		display: flex;
		align-items: center;
		gap: 1em;
	}

	button {
		font-size: 8em;
		width: 1em;
		height: 1em;
	}

	svg {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		left: 0;
	}

	.duration {
		flex: 1;
		height: 1em;
		background: #ccc;
	}

	.remaining {
		position: absolute;
		width: calc(100% * var(--p));
		height: 100%;
		background: #999;
	}
</style>
