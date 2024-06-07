<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import MoveItemsBtwContainers from '$lib/components/gsap-examples/flip/move-items-btw-containers/move-items-btw-containers.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Moving Items Between Containers"
		description="Click the button to animate the items between the containers"
	/>

	<section class="pb-20 w-full h-full flex flex-col items-center gap-y-5">
		<MoveItemsBtwContainers />
	</section>
</main>
