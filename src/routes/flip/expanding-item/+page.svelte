<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import ExpandingItem from '$lib/components/gsap-examples/flip/expanding-item/expanding-item.svelte';
	import MoveItemsBtwContainers from '$lib/components/gsap-examples/flip/move-items-btw-containers/move-items-btw-containers.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Click on cards to expand them"
		description="Uses Flip animations to expand the cards smoothly"
	/>

	<section class="pb-20 w-full h-full flex flex-col items-center gap-y-5">
		<ExpandingItem />
	</section>
</main>
