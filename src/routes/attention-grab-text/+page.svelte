<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import AttentionGrabText from '$lib/components/gsap-examples/attention-grab-text/attention-grab-text.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero title="Attention Grabbing Text" description="Also called Machine Gun Text" />

	<section class="p-10 w-full h-full flex justify-center">
		<AttentionGrabText />
	</section>
</main>
