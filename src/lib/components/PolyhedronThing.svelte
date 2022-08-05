<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';

	const verticesOfCube = [
    -1,-1,-1,    1,-1,-1,    1, 1,-1,    -1, 1,-1,
    -1,-1, 1,    1,-1, 1,    1, 1, 1,    -1, 1, 1,
	];

	const indicesOfFaces = [
	    2,1,0,    0,3,2,
	    0,4,7,    7,3,0,
	    0,1,5,    5,4,0,
	    1,2,6,    6,5,1,
	    2,3,7,    7,6,2,
	    4,5,6,    6,7,4
	];
</script>

<SC.Mesh 
	geometry={new THREE.PolyhedronGeometry( verticesOfCube, indicesOfFaces, 6, 0 )}
	material={new THREE.MeshLambertMaterial({ color: 'coral', side: THREE.DoubleSide })}
/>