<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import VerticalHorizontalTransitions from '$lib/components/gsap-examples/scroll-trigger/vertical-horizontal-transitions/vertical-horizontal-transitions.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Scroll Trigger Vertical Horizontal Transitions"
		description="Just Scroll inside the container"
	/>

	<section class="p-10 w-full h-full flex flex-col items-center gap-y-5 overflow-x-hidden">
		<VerticalHorizontalTransitions />
	</section>
</main>
