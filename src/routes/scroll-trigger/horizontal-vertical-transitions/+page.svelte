<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import HorizontalVerticalTransitions from '$lib/components/gsap-examples/scroll-trigger/horizontal-vertical-transitions/horizontal-vertical-transitions.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Scroll Trigger Horizontal Vertical Transitions"
		description="Just Scroll inside the container"
	/>

	<section class="p-10 w-full h-full flex flex-col items-center gap-y-5 overflow-x-hidden">
		<HorizontalVerticalTransitions />
	</section>
</main>
