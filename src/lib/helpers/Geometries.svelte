<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

	export let open = false

	let showXYPlane = false
	let showYZPlane = false
	let showZXPlane = false
</script>

{#if showXYPlane}
	<SC.Mesh
		geometry={new THREE.PlaneGeometry(30, 30)}
		material={new THREE.MeshLambertMaterial({ color: 'steelblue', side: THREE.DoubleSide })}
		rotation={[0, 0, 0]}
	/>
{/if}

{#if showYZPlane}
	<SC.Mesh
		geometry={new THREE.PlaneGeometry(30, 30)}
		material={new THREE.MeshLambertMaterial({ color: 'steelblue', side: THREE.DoubleSide })}
		rotation={[0, Math.PI / 2, 0]}
	/>
{/if}

{#if showZXPlane}
	<SC.Mesh
		geometry={new THREE.PlaneGeometry(30, 30)}
		material={new THREE.MeshLambertMaterial({ color: 'steelblue', side: THREE.DoubleSide })}
		rotation={[Math.PI / 2, 0, 0]}
	/>
{/if}

<!-- 	<SC.Mesh
	geometry={new THREE.CylinderGeometry(1, 1, 10, 16)}
	material={new THREE.MeshLambertMaterial({ color: 'brown' })}
	rotation={[0, 0, 0]}
	position={[0, 0.01, 0]}
/> -->

<!-- <SC.Mesh
	geometry={new THREE.SphereGeometry(0.2)}
	material={new THREE.MeshLambertMaterial({ color: 'black', wireframe: true })}
	rotation={[0, 0, 0]}
	position={[0, 0.01, 0]}
/> -->

<section class="flow" class:open>
	<button 
		type="button" 
		class="toggler"
		on:click={() => open = !open}
	>
		<span aria-hidden="true" class="toggler-icon">&#9001;</span>
	</button>

	<h2>Geometry Toggler</h2>

	<div class="flow">
		<div>
			<label for="showXYPlane">showXYPlane </label>
			<input type="checkbox" bind:checked={showXYPlane} id="showXYPlane" />
		</div>
		<div>
			<label for="showYZPlane">showYZPlane </label>
			<input type="checkbox" bind:checked={showYZPlane} id="showYZPlane" />
		</div>
		<div>
			<label for="showZXPlane">showZXPlane </label>
			<input type="checkbox" bind:checked={showZXPlane} id="showZXPlane" />
		</div>
	</div>
</section>

<style>
	section {
		--flow-space: 0.5rem;

		position: absolute;
		top: 3rem;
		right: 0;
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
</style>