<script lang="ts">
	const { src = '', title = '' } = $props();
</script>

<div
	class="card card-compact w-96 bg-base-300 shadow-xl shadow-secondary/40 cursor-pointer hover:scale-105 duration-300"
>
	<figure class="">
		<img {src} alt="Bananas" />
	</figure>
	<div class="card-body">
		<h2 class="card-title">{title}</h2>
		<p class="text-lg">Click to learn more</p>
	</div>
</div>
