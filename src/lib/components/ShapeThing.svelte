<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

	const colors = [1, 2, 3, 4, 5, 6]
	const points = Array.from({ length: colors.length }, (_, i) => (new THREE.Vector2( i, i )))
	const thing = new THREE.Shape(points)
</script>