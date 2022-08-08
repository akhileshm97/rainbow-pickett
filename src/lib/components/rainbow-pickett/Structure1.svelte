<script>
	import * as SC from 'svelte-cubed';

	import RainbowPickett from './RainbowPickett.svelte'

	export let wireframe = false
	let rotateY = 0

	let scale = 2
</script>

<SC.Group rotation={[0, rotateY, 0]} position={[1, 0,0]} >
	<RainbowPickett {wireframe} {scale} rotation={{ x: 0, y: 0, z: 0 }} />
	<RainbowPickett {wireframe} {scale} rotation={{ x: Math.PI, y: 0, z: 0 }} />
	<RainbowPickett {wireframe} {scale} rotation={{ x: Math.PI / 2, y: 0, z: 0 }} />
	<RainbowPickett {wireframe} {scale} rotation={{ x: Math.PI / -2, y: 0, z: 0 }} />
</SC.Group>

<SC.Group rotation={[0, 0, Math.PI]} position={[-1, 0, 0]}>
	<RainbowPickett {wireframe} {scale} rotation={{ x: 0, y: 0, z: 0 }} />
	<RainbowPickett {wireframe} {scale} rotation={{ x: Math.PI, y: 0, z: 0 }} />
	<RainbowPickett {wireframe} {scale} rotation={{ x: Math.PI / 2, y: 0, z: 0 }} />
	<RainbowPickett {wireframe} {scale} rotation={{ x: Math.PI / -2, y: 0, z: 0 }} />
</SC.Group>