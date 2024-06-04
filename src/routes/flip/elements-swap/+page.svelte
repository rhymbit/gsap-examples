<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import ElementsSwap from '$lib/components/gsap-examples/flip/elements-swap/elements-swap.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero title="Elements Swap Positions" description="Click anywhere inside the box" />

	<section class="p-20 w-full h-full flex justify-center">
		<ElementsSwap />
	</section>
</main>
