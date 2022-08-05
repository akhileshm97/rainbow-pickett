<script>
	import * as SC from 'svelte-cubed';

	import Structure1 from "./Structure1.svelte";
	import Structure2 from "./Structure2.svelte";
	import Structure3 from "./Structure3.svelte";
	import Structure4 from "./Structure4.svelte";

	export let rotateY = 0

	// let wireframe = false
</script>

<SC.Group rotation={[0, rotateY, 0]}>
	<Structure1 />
	<Structure2 />
	<Structure3 />
	<Structure4 />
</SC.Group>

<!-- <button type='button' on:click={() => wireframe = !wireframe}>toggle wireframes</button> -->

<!-- <style>
	button {
		position: absolute;
		bottom: 0;
		right: 0;
	}
</style> -->