<script lang="ts">
	/**
	 * Inspired by - https://codepen.io/GreenSock/pen/Yzdzxem
	 * Uses GSAP's Flip plugin to animate the cards in a slider
	 */
	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import { onMount } from 'svelte';

	onMount(() => {
		gsap.registerPlugin(Flip);
	});

	let slider: HTMLElement | null = null;

	function moveCard() {
		// get the last card from the HTML
		// initially it will be `<div class="card-slider-card bg-teal-700">1</div>`
		const lastCard = slider?.querySelector('.card-slider-card:last-child') as HTMLDivElement;

		if (slider && lastCard) {
			// hide the last card
			// When we hide the card (i.e., remove it from document flow), the `onLeave` callback from Flip gets called
			lastCard.style.display = 'none';
			// now create a new card with the same content and class
			// but insert it at the beginning, i.e, before `<div class="card-slider-card bg-rose-700">5</div>`
			// When a new card is inserted the `onEnter` callback from Flip gets called
			const newCard = document.createElement('div');
			newCard.className = lastCard.className;
			newCard.textContent = lastCard.textContent;
			slider.insertBefore(newCard, slider.firstChild);
		}
	}

	function onClick() {
		let state = Flip.getState('.card-slider-card');

		moveCard();

		Flip.from(state, {
			targets: '.card-slider-card',
			ease: 'sine.inOut',
			absolute: true,
			// Checkout comments inside the `moveCard()` function to learn more about `onEnter` and `onLeave`
			onEnter: (elements) => {
				return gsap.from(elements, {
					yPercent: 20,
					opacity: 0
				});
			},
			onLeave: (elements) => {
				return gsap.to(elements, {
					yPercent: 20,
					xPercent: -20,
					transformOrigin: 'bottom left',
					opacity: 0,
					onComplete() {
						slider?.removeChild(elements[0]);
					}
				});
			}
		});
	}
</script>

<section
	on:click={onClick}
	role="none"
	class="w-[600px] h-[600px] px-40 pb-28 flex justify-start items-center ring-2 ring-base-content rounded-box cursor-pointer"
>
	<section bind:this={slider} class="relative">
		<div class="card-slider-card bg-rose-700">5</div>
		<div class="card-slider-card bg-sky-700">4</div>
		<div class="card-slider-card bg-pink-700">3</div>
		<div class="card-slider-card bg-amber-700">2</div>
		<div class="card-slider-card bg-teal-700">1</div>
	</section>
</section>

<style>
	.card-slider-card {
		@apply absolute w-56 aspect-square flex items-center justify-center text-3xl rounded-box shadow shadow-base-content;
	}

	/* 
		This 👇🏻 could be done with code, but I did it manually for clarity
	*/

	.card-slider-card:nth-child(5) {
		left: 0;
		top: 0;
	}
	.card-slider-card:nth-child(4) {
		left: 20px;
		top: -20px;
	}
	.card-slider-card:nth-child(3) {
		left: 40px;
		top: -40px;
	}
	.card-slider-card:nth-child(2) {
		left: 60px;
		top: -60px;
	}
	.card-slider-card:nth-child(1) {
		left: 80px;
		top: -80px;
	}
</style>
