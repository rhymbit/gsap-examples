<script lang="ts">
	/**
	 * Inspired from - https://codepen.io/GreenSock/pen/OJNYjmz
	 * Uses GSAP Flip plugin to animate the elements swap
	 */

	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import { onMount } from 'svelte';

	let container: HTMLElement | null = null;
	let elementsGsapArray: HTMLElement[] = [];

	onMount(() => {
		gsap.registerPlugin(Flip);
		elementsGsapArray = gsap.utils.toArray(document.querySelectorAll('[data-element]'));
	});

	function swap() {
		const state = Flip.getState(elementsGsapArray);

		if (container && elementsGsapArray && state) {
			// swap the squares
			elementsGsapArray[0] === container.children[0]
				? container.appendChild(elementsGsapArray[0])
				: container.appendChild(elementsGsapArray[1]);

			Flip.from(state, {
				duration: 2,
				ease: 'power1.inOut'
			});
		}
	}
</script>

<section
	class="px-4 py-20 w-full flex justify-between items-center border-2 rounded-box cursor-pointer"
	bind:this={container}
	role="none"
	on:click={swap}
>
	<div data-element class="bg-primary text-primary-content">1</div>
	<div data-element class="bg-secondary text-secondary-content">2</div>
</section>

<style>
	[data-element] {
		@apply w-28 flex justify-center items-center aspect-square rounded-box shadow shadow-base-content;
	}
</style>
