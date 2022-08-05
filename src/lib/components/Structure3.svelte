<script>
	import * as SC from 'svelte-cubed';

	import RainbowPickett from './RainbowPickett.svelte'

	export let wireframe = false
</script>

<SC.Group rotation={[0, Math.PI / 2, 0]} position={[-60, 0, 41]}>
	<RainbowPickett {wireframe} rotation={{ x: 0, y: 0, z: 0 }} />
	<!-- <RainbowPickett {wireframe} rotation={{ x: Math.PI, y: 0, z: 0 }} /> -->
	<RainbowPickett {wireframe} rotation={{ x: Math.PI / 2, y: 0, z: 0 }} />
	<!-- <RainbowPickett {wireframe} rotation={{ x: Math.PI / -2, y: 0, z: 0 }} /> -->
</SC.Group>

<SC.Group rotation={[0, Math.PI / -2, 0]} position={[-60, 0, 40]}>
	<!-- <RainbowPickett {wireframe} rotation={{ x: 0, y: 0, z: 0 }} /> -->
	<RainbowPickett {wireframe} rotation={{ x: Math.PI, y: 0, z: 0 }} />
	<!-- <RainbowPickett {wireframe} rotation={{ x: Math.PI / 2, y: 0, z: 0 }} /> -->
	<RainbowPickett {wireframe} rotation={{ x: Math.PI / -2, y: 0, z: 0 }} />
</SC.Group>