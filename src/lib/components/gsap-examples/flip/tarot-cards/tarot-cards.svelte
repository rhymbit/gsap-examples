<script lang="ts">
	/**
	 * Inspired from - https://codepen.io/cassie-codes/pen/wvyRWaB
	 * Uses GSAP Flip plugin to animate the tarot cards
	 */

	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import { onMount } from 'svelte';
	import card1 from './assets/card1.svg';
	import card2 from './assets/card2.svg';
	import card3 from './assets/card3.svg';
	import card4 from './assets/card4.svg';
	import crystalBall from './assets/crystal-ball.svg';

	// selection array of card sources
	const cards = [card1, card2, card3, card4];

	onMount(() => {
		gsap.registerPlugin(Flip);
	});

	// table element reference
	let table: HTMLElement | null = null;

	function createCard() {
		// save the state
		const state = Flip.getState('.card-tarot');
		// make dom changes - create a new card & add it to the table
		let random = gsap.utils.random(0, 3, 1);
		let card = document.createElement('img');
		card.src = cards[random];
		card.classList.add('card-tarot');
		// we also have to manually add the event listener to the new card
		card.addEventListener('click', (e) => {
			e.stopPropagation();
			const state = Flip.getState('.card-tarot');
			card.classList.add('card-tarot-exiting');
			flipCardsState(state);
		});
		table?.appendChild(card);
		// call Flip.from()
		flipCardsState(state);
	}

	function shuffleCards() {
		// save the state
		const state = Flip.getState('.card-tarot');
		// make dom changes - shuffle the cards
		const dealtCards = gsap.utils.toArray('.card-tarot');
		gsap.utils.shuffle(dealtCards).forEach((card) => table?.appendChild(card as HTMLElement));
		// call Flip.from()
		flipCardsState(state);
	}

	function destroyCard(
		e: MouseEvent & {
			currentTarget: EventTarget & HTMLImageElement;
		}
	) {
		// stop the event from bubbling up to the table
		e.stopPropagation();
		// save the state
		const state = Flip.getState('.card-tarot');
		// make dom changes - remove the card
		e.currentTarget.classList.add('card-tarot-exiting');
		// call Flip.from()
		flipCardsState(state);
	}

	function flipCardsState(state: Flip.FlipState) {
		Flip.from(state, {
			targets: '.card-tarot',
			ease: 'sine.inOut',
			absolute: true,
			onEnter: (elements) => {
				return gsap.from(elements, {
					yPercent: 100,
					opacity: 0,
					ease: 'sine.out'
				});
			},
			onLeave: (elements) => {
				return gsap.to(elements, {
					scale: 0.3,
					rotation: 360,
					opacity: 0,
					ease: 'sine.out'
				});
			}
		});
	}
</script>

<section class="w-full flex-1 flex flex-col items-center justify-between">
	<!-- table -->
	<section
		bind:this={table}
		onclick={shuffleCards}
		class="pt-7 w-full max-w-7xl h-[400px] bg-accent/50 flex justify-center cursor-pointer"
		role="none"
	>
		{#each cards as card}
			<img src={card} class="card-tarot" alt="" onclick={destroyCard} role="none" />
		{/each}
	</section>

	<!-- crystal ball -->
	<button onclick={createCard}>
		<img src={crystalBall} class="w-40" alt="" />
	</button>
</section>

<style>
	:global(.card-tarot) {
		@apply h-44 cursor-pointer;
	}

	:global(.card-tarot-exiting) {
		@apply hidden;
	}
</style>
