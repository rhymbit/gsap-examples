<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import LayoutChange from '$lib/components/gsap-examples/flip/layout-change/layout-change.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero title="Flipping Layout Changes" description="Just enjoy the animations" />

	<section class="pb-20 w-full h-full flex flex-col items-center gap-y-5">
		<LayoutChange />
	</section>
</main>
