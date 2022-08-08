<script>
// @ts-nocheck
	import { onMount, createEventDispatcher } from 'svelte';
	import { tweened } from 'svelte/motion';
	import { cubicOut, cubicInOut } from 'svelte/easing';
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

	import Structure from '$lib/components/rainbow-pickett/Structure.svelte'
	// import CameraControls from '$lib/helpers/CameraControls.svelte'
	// import FieldMarkers from '$lib/helpers/FieldMarkers.svelte'

	const dispatch = createEventDispatcher();

	export let current, introFinished

	export const startIntro = () => {
		setTimeout(() => {
			camX.set(-70)
			camY.set(0)
			camZ.set(0)
		}, 1000)
		setTimeout(() => {
			camX.set(70)
			camY.set(0)
			camZ.set(0)
		}, 3000)
		setTimeout(() => {
			camX.set(70)
			camY.set(0)
			camZ.set(120)
		}, 5000)
		setTimeout(() => {
			camX.set(0)
			camY.set(30) 
			camZ.set(180)
		}, 7000)
		setTimeout(() => {
			dispatch('introfinished', 'intro finished')
		}, 9000)
	}

	const rotateY = tweened(0, { duration: 1000, easing: cubicOut	});

	const camX = tweened(-70, { duration: 2000, easing: cubicInOut });
	const camY = tweened(0, { duration: 2000, easing: cubicInOut });
	const camZ = tweened(120, { duration: 2000, easing: cubicInOut });

	const camTargetX = tweened(0, { duration: 1000, easing: cubicInOut });
	const camTargetY = tweened(0, { duration: 1000, easing: cubicInOut });
	const camTargetZ = tweened(0, { duration: 1000, easing: cubicInOut });

	const camOptions = {
		overview: {
			cam: { x: 0, y: 30, z: 180 },
			camTarget: { x: 0, y: 0, z: 0 }
		},
		structure1: {
			cam: { x: 0, y: 0, z: 60 },
			camTarget: { x: 0, y: 0, z: 0 }
		},
		structure2: {
			cam: { x: 0, y: 0, z: 60 },
			camTarget: { x: 60, y: 0, z: 40 }
		},
		structure4: {
			cam: { x: 20, y: -20, z: 70 },
			camTarget: { x: -20, y: -30, z: 45 }
		}
	}
	
	let autoRotate = false

	$: updateCamera(current)

	function updateCamera(structure) {
		if(introFinished) {
			camTargetX.set(camOptions[structure].camTarget.x)
			camTargetY.set(camOptions[structure].camTarget.y)
			camTargetZ.set(camOptions[structure].camTarget.z)

			camX.set(camOptions[structure].cam.x)
			camY.set(camOptions[structure].cam.y)
			camZ.set(camOptions[structure].cam.z)
		}
	}

	SC.onFrame(() => {
		if(autoRotate) {
			rotateY.set($rotateY + 0.02)
		}
	})

	onMount(() => {
		dispatch('mount', 'structure mounted')
	})
</script>

<SC.Canvas
	antialias
	background={new THREE.Color('papayawhip')}
	fog={new THREE.FogExp2('papayawhip', 0.005)}
	shadows
>
	<SC.PerspectiveCamera 
		position={[$camX, $camY, $camZ]} 
		target={[$camTargetX, $camTargetY, $camTargetZ]} 
	/>
<!-- 	<SC.OrbitControls 
		enableZoom={true} 
		maxPolarAngle={Math.PI * 0.95} 
		minDistance={1}
		maxDistance={200}
		enableDamping 
		dampingFactor={0.1}
		zoomSpeed={0.5} 
	/> -->
	<SC.AmbientLight intensity={0.6} />
	<SC.DirectionalLight intensity={0.6} position={[20, 40, 80]} shadow={{ mapSize: [2048, 2048] }} />

	<Structure rotateY={$rotateY} />

	<!-- <FieldMarkers /> -->
	<!-- <CameraControls {camX} {camY} {camZ} open={false} /> -->
</SC.Canvas>
