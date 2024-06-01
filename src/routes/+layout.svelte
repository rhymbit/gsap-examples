<script lang="ts">
	import Navbar from '$lib/components/navbar/navbar.svelte';
	import '../app.css';
</script>

<svelte:head>
	<title>GSAP Examples</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Ubuntu+Sans+Mono:ital,wght@0,400..700;1,400..700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<main class="w-full h-full flex flex-col justify-center items-center">
	<Navbar />
	<slot />
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Sans+Mono:ital,wght@0,400..700;1,400..700&display=swap');

	:global(body) {
		font-family: 'Ubuntu Sans Mono', sans-serif;
		font-weight: 400;
		font-style: normal;
		font-size: 4rem;
		width: 100vw;
		min-height: 100vh;
	}
</style>
