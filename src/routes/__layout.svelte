<script lang="ts">
	import Loading from "$lib/misc/Loading.svelte";

	import '../css/modern-css-reset.min.css';
	import '../css/utilities.css';
	import '../css/base.css';
	import '../css/styles.css';
	import '../app.css';
</script>

<main>
	<slot />
</main>

<Loading />
