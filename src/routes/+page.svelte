<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
</script>

<main class="w-full h-full flex flex-col items-center">
	<ExamplePageHero
		title="Collection of GSAP Examples"
		description="My collection of GSAP examples with SvelteKit"
	/>

	<p class="text-xl animate-pulse">Use Navbar to navigate to the different GSAP examples.</p>
	<p class="text-xl animate-pulse">
		Detailed explanations for animations are inside the source code
	</p>
</main>
