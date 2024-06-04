<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import CardsSlider from '$lib/components/gsap-examples/flip/cards-slider/cards-slider.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Cards Slider"
		description="Click anywhere inside the box to move the cards with a Flip effect"
	/>

	<section class="p-20 w-full h-full flex justify-center">
		<CardsSlider />
	</section>
</main>
