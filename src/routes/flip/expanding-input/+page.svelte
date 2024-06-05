<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import ExpandingInput from '$lib/components/gsap-examples/flip/expanding-input/expanding-input.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Smooth Exapanding Input"
		description="Start typing inside the input field to see it expand."
	/>

	<section class="p-20 w-full h-full flex justify-center">
		<ExpandingInput />
	</section>
</main>
