<script>
// @ts-nocheck

	import { onMount } from 'svelte';

	import Scene from "$lib/Scene.svelte";
	import Loading from "$lib/Loading.svelte";
	import Hero from "$lib/components/Hero.svelte";
	import Section1 from "$lib/components/Section1.svelte";
	import Section2 from "$lib/components/Section2.svelte";
	import Section3 from "$lib/components/Section3.svelte";
	import Disclaimer from '$lib/components/Disclaimer.svelte';

	const structureMap = {
		hero: 'overview',
		section1: 'structure4',
		section2: 'structure2',
		section3: 'structure1'
	}

	let loading = false
	let current = 'section1'
	let introFinished = false
	let structureScene

	onMount(() => {
		const sections = document.querySelectorAll('.page-section')

		const ioCallback = (entries) => {
		  entries.forEach(entry => {
				if (entry.isIntersecting) {
		      current = structureMap[entry.target.id]
				}
		  });
		}

		const ioOptions = {
			threshold: 0.6
		}

		const setDetails = (target) => {
			const io = new IntersectionObserver(ioCallback, ioOptions);
			io.observe(target)
		}

		sections.forEach(setDetails)
	})
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<div 
	class="container"
	aria-describedby="progress-bar" 
	aria-hidden={loading ? 'true' : 'false'}
> 
	<div id="structure-scene">
		<Scene 
			bind:this={structureScene}
			{current} 
			{introFinished}
			on:mount={() => loading = false} 
			on:introfinished={() => introFinished = true}
		/>
	</div>

	{#if loading}
		<Loading />
	{/if}

	<Disclaimer on:proceed={structureScene.proceed} />

	<div class="page" class:show={introFinished}>
		<Hero />
		<Section1 />
		<Section2 />
		<Section3 />
	</div>
</div>

<style>
	.container {
		position: relative;
		height: 100vh;
		/*overscroll-behavior: contain;*/
	}
	.page {
		scroll-snap-type: y mandatory;
		height: 100%;
		overflow-y: auto;
		visibility: hidden;
		opacity: 0;
		transition: visibility 0.5s, opacity 0.5s;
	}
	.page.show {
		visibility: visible;
		opacity: 1;
	}
	:global(.page > *) {
		scroll-snap-align: start;
	}
	:global(.highlight) {
		outline: 4px solid black;
		outline-offset: -10px;
	}

	#structure-scene {
		position: fixed;
		z-index: -1;
		min-height: 100vh;
		width: 100%;
	}
</style>