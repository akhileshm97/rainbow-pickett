<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

	export let position = { x: 0, y: 0, z: 0 }
	export let rotation = { x: 0, y: 0, z: 0 }
	export let scale = 1
	export let wireframe = false

	// SC.onFrame(() => rotateY += 0.01)

	const colors = ['#d7dece', '#89c7d6', '#b498bd', '#cf7775', '#fc7d3a', '#c99429']
	// longestShortLength is the basis for all position calculations (basis or base?)
	const longestShortLength = 12
	// frameWidth is used for extending top side as well
	const frameWidth = 1

	const trapezoids = colors.map((color, i) => {
		const shortLength = longestShortLength - (i * 2)
		const longLength = shortLength + (2 * frameWidth)

		return ({
			shortLength,
			color,
			x: frameWidth * i * 2,
			y: (shortLength / 2) / Math.SQRT2,
			z: (shortLength / 2) / Math.SQRT2,
			sides: [
				{ // top
					shape: new THREE.Shape([
						new THREE.Vector2( 0, longLength / -2 ),
						new THREE.Vector2( frameWidth, longLength / -2 ),
						new THREE.Vector2( frameWidth, longLength / 2 ),
						new THREE.Vector2( 0, longLength / 2 )
					]), 
					rotateY: 0, 
					pos: { x: 0, y: 0, z: frameWidth } 
				},
				{ // bpttom
					shape: new THREE.Shape([
						new THREE.Vector2( 0, shortLength / -2 ),
						new THREE.Vector2( frameWidth, shortLength / -2 ),
						new THREE.Vector2( frameWidth, shortLength / 2 ),
						new THREE.Vector2( 0, shortLength / 2 )
					]), 
					rotateY: Math.PI, 
					pos: { x: frameWidth, y: 0, z: 0 }
				}, 
				{ // left
					shape: new THREE.Shape([
						new THREE.Vector2( 0, shortLength / -2 ),
						new THREE.Vector2( frameWidth, longLength / -2 ),
						new THREE.Vector2( frameWidth, longLength / 2 ),
						new THREE.Vector2( 0, shortLength / 2 )
					]), 
					rotateY: Math.PI / -2, 
					pos: { x: 0, y: 0, z: 0 }
				}, 
				{ // right
					shape: new THREE.Shape([
						new THREE.Vector2( 0, longLength / -2 ),
						new THREE.Vector2( frameWidth, shortLength / -2 ),
						new THREE.Vector2( frameWidth, shortLength / 2 ),
						new THREE.Vector2( 0, longLength / 2 )
					]), 
					rotateY: Math.PI / 2, 
					pos: { x: frameWidth, y: 0, z: frameWidth }
				} 
			]
		})
	})
</script>

<SC.Group 
	position={[position.x, position.y, position.z]} 
	rotation={[rotation.x, rotation.y, rotation.z]}
	scale={[scale, scale, scale]}
>
	{#each trapezoids as zoid}
		<SC.Group 
			position={[zoid.x, zoid.y, zoid.z]}
			rotation={[Math.PI / -4, 0, 0]}
		>
			{#each zoid.sides as side}
				<SC.Mesh 
					material={new THREE.MeshLambertMaterial({ color: zoid.color, side: THREE.DoubleSide, wireframe })}
					geometry={new THREE.ShapeGeometry(side.shape)}
					position={[side.pos.x, side.pos.y, side.pos.z]}	
					rotation={[0, side.rotateY, 0]}
				/>
			{/each}
					<!-- geometry={new THREE.PlaneGeometry(frameWidth, zoid.shortLength)} -->
		</SC.Group>
	{/each}
</SC.Group>
