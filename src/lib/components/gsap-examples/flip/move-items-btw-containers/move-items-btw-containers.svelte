<script lang="ts">
	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import { onMount } from 'svelte';

	onMount(() => {
		gsap.registerPlugin(Flip);
	});

	let container1: HTMLElement;
	let container2: HTMLElement;

	function moveItems() {
		let items = gsap.utils.toArray(document.querySelectorAll('.item') ?? []) as HTMLElement[];

		if (items.length > 0) {
			const state = Flip.getState(items);

			// mix the order
			gsap.utils.shuffle(items);

			// move items between containers
			if (items[0].parentElement === container1) {
				items.forEach((item) => container2.appendChild(item));
			} else {
				items.forEach((item) => container1.appendChild(item));
			}

			// animate
			Flip.from(state, {
				duration: 0.9,
				stagger: 0.09,
				ease: 'back.out(1.7)'
			});
		}
	}
</script>

<button onclick={moveItems} class="btn btn-secondary"> Move Items </button>

<section class="flex items-center justify-center gap-28">
	<section bind:this={container1} class="container container-one">
		<div class="item">Item1</div>
		<div class="item">Item2</div>
		<div class="item">Item3</div>
		<div class="item">Item4</div>
		<div class="item">Item5</div>
	</section>

	<section bind:this={container2} class="container container-two"></section>
</section>

<style>
	.container {
		@apply px-2 py-4 flex flex-col w-40 h-72 text-lg border-4 rounded-box;

		&.container-one {
			@apply border-primary;
		}

		&.container-two {
			@apply border-secondary;
		}

		.item {
			@apply text-center rounded-box py-2 mb-2;
		}

		.item:nth-child(1) {
			@apply bg-teal-700;
		}

		.item:nth-child(2) {
			@apply bg-amber-700;
		}

		.item:nth-child(3) {
			@apply bg-sky-700;
		}

		.item:nth-child(4) {
			@apply bg-fuchsia-700;
		}

		.item:nth-child(5) {
			@apply bg-rose-700;
		}
	}
</style>
