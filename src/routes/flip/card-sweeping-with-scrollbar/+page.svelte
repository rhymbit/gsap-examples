<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import CardSweepingWithScroll from '$lib/components/gsap-examples/flip/card-sweeping-with-scroll/card-sweeping-with-scroll.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Card Sweeping with ScrollTrigger"
		description="You scroll and the card moves smoothly with the scroll"
	/>

	<section class="p-20 w-full h-full flex">
		<CardSweepingWithScroll />
	</section>
</main>
