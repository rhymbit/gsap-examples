<script lang="ts">
	import ExamplePageHero from '$lib/components/example-page-hero/example-page-hero.svelte';
	import PhotoGallery from '$lib/components/gsap-examples/flip/photo-gallery/photo-gallery.svelte';
</script>

<main class="w-full h-full">
	<ExamplePageHero
		title="Photo Gallery"
		description="Click on photographs to test Flip animations."
	/>

	<section class="pb-20 w-full h-full flex flex-col items-center gap-y-5">
		<PhotoGallery />
	</section>
</main>
