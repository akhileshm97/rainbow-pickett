<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let open = true

	const onClick = () => {
		open = false
		dispatch('proceed', 'proceeding with site')
	}
</script>

<div class='dialog-container' class:closed={!open}>
	<div class='flow dialog'>
		<p>This project is only meant to showcase my skills in web development. No Copywright infringment is intended. Original artist is credited and link of description of the art is provided.</p>

		<p>You can check out my other work at my GitHub profile: 
			<br />
			<a href="https://github.com/akhileshm97" target="_blank">Akhilesh Manuvarthi</a>
		</p>

		<button type="button" on:click={onClick}>Proceed</button>
	</div>
</div>

<style>
	.dialog-container {
		position: absolute;
		inset: 0;
		z-index: 2;
		display: grid;
		background-color: black;
		place-content: center;
		padding: 2rem;
		/*margin: 10vw;*/
	}
	.dialog-container.closed {
		display: none;
	}

	.dialog {
		background-color: white;
		padding: 2rem;
		max-width: 60ch;
	}

	button {
		display: block;
		color: white;
		background-color: black;
		padding: 0.5em 1em;
		border: none;
		border-radius: 0.25em;
		margin-left: auto;
		margin-right: auto;
		cursor: pointer;
	}
</style>