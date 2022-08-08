<script>
	import { fade } from 'svelte/transition'

	import { loading } from '$lib/stores.js';
</script>

{#if $loading}
	<div in:fade={{ duration: 50 }} out:fade={{ duration: 50 }}>
		<!-- {message[status]} -->
		Loading...
	</div>
{/if}

<style>
	div {
		position: absolute;
		z-index: 30;
		inset: 0;
		display: grid;
		place-content: center;
		color: white;
		background-color: hsla(0, 0%, 0%, 1);
		font-size: 4rem;
		font-family: monospace;
		padding: 1em 2em;
		user-select: none;
	}
</style>