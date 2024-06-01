<script lang="ts">
	let { title = '', description = '' } = $props();
</script>

<section class="p-20 w-full h-full flex flex-col items-center justify-center">
	<h1 class="text-4xl font-bold text-center">{title}</h1>
	<p class="mt-4 text-lg text-center">{description}</p>
</section>
