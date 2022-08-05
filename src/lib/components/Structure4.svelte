<script>
	import * as SC from 'svelte-cubed';
	import * as THREE from 'three';

	import RainbowPickett from './RainbowPickett.svelte'
</script>

<SC.Group position={[-10, -30, 45]}>
	<SC.Mesh 
		geometry={new THREE.PlaneGeometry(20, 20)}
		material={new THREE.MeshLambertMaterial({ color: 'blanchedalmond', side: THREE.DoubleSide })}
		position={[9, 10, 0]}
	/>
	<SC.Mesh 
		geometry={new THREE.PlaneGeometry(20, 20)}
		material={new THREE.MeshLambertMaterial({ color: 'blanchedalmond', side: THREE.DoubleSide })}
		position={[9, 0, 10]}
		rotation={[Math.PI / -2, 0, 0]}
	/>
	<SC.Mesh 
		geometry={new THREE.PlaneGeometry(20, 20)}
		material={new THREE.MeshLambertMaterial({ color: 'blanchedalmond', side: THREE.DoubleSide })}
		position={[-1, 10, 10]}
		rotation={[0, Math.PI / -2, 0]}
	/>

	<RainbowPickett scale={1} rotation={{ x: 0, y: 0, z: 0 }} />
</SC.Group>
 <!-- position={{ x: 0, y: 0, z: 90 }} -->