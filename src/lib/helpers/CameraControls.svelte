<script>
	export let camX, camY, camZ, open = true

	let x, y, z

	function ranCam() { 
		camX.set(Math.round(Math.random() * 50) * (Math.random() < 0.5 ? 1 : -1)) 
		camY.set(Math.round(Math.random() * 50)) 
		camZ.set((Math.round(Math.random() * 50) * (Math.random() < 0.5 ? 1 : -1))) 
	}

	function changeCam() {
		camX.set(x)
		camY.set(y)
		camZ.set(z)
	}
</script>

<section class="flow" class:open>
	<button 
		type="button" 
		class="toggler"
		on:click={() => open = !open}
	>
		<span aria-hidden="true" class="toggler-icon">&#9001;</span>
	</button>

	<h2>Camera Controls</h2>

	<button 
		type="button" 
		on:click={ranCam}
	>randomize</button>

	<hr />

	<div class="flow">
		<div>
			<label for="x">x </label>
			<input type="number" bind:value={x} id="x" />
		</div>
		<div>
			<label for="y">y </label>
			<input type="number" bind:value={y} id="y" />
		</div>
		<div>
			<label for="z">z </label>
			<input type="number" bind:value={z} id="z" />
		</div>
	</div>

	<button 
		type="button" 
		on:click={changeCam}
	>change</button>
</section>

<style>
	section {
		--flow-space: 0.5rem;

		position: absolute;
		top: 0;
		right: 0;
		z-index: 2;
		color: white;
		background-color: black;
		text-align: center;
		padding: 1rem;
		transform: translateX(100%);
		transition: transform 0.5s cubic-bezier(.77,0,.18,1);
	}
	section.open {
		transform: translateX(0);
	}

	h2 {
		font-size: 1.25rem;
	}

	button {
		display: block;
		color: white;
		background-color: darkslateblue;
		padding: 0.5em 1em;
		border: none;
		margin-left: auto;
		margin-right: auto;
	}

	.toggler {
		position: absolute;
		top: 0;
		right: 100%;
		color: white;
		background-color: black;
		border: 2px solid #333333;
	}
	.toggler-icon {
		display: inline-block;
		transition: transform 0.5s cubic-bezier(.77,0,.18,1);
	}
	section.open .toggler-icon {
		transform: rotate(0.5turn);
	}

	input {
		max-width: 10ch;
	}
</style>