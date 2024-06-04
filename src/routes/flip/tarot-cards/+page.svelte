<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import TarotCards from '$lib/components/gsap-examples/flip/tarot-cards/tarot-cards.svelte';
</script>

<main class="w-full h-full min-h-screen flex flex-col">
	<ExamplePageHero
		title="Tarot Cards"
		description="Click on table, click on cards, click on crystal ball to see the magic!"
	/>

	<section class="px-20 w-full h-full flex-1 flex flex-col items-center">
		<TarotCards />
	</section>
</main>
