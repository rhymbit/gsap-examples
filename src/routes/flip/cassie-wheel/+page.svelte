<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import CassieWheel from '$lib/components/gsap-examples/flip/cassie-wheel/cassie-wheel.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero title="Cassie Wheel" description="Scroll to spin the wheel." />

	<section class="pb-20 w-full h-full flex flex-col items-center gap-y-5">
		<CassieWheel />
	</section>
</main>
