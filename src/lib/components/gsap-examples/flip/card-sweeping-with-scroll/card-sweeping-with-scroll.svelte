<script lang="ts">
	/**
	 * Inspired by - https://codepen.io/GreenSock/pen/bGxOjeP
	 * Uses GSAP's Flip plugin to animate the card background
	 */
	import gsap from 'gsap';
	import { Flip } from 'gsap/dist/Flip';
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';
	import { onDestroy, onMount } from 'svelte';

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, Flip);
		// initialize the animation properties
		anim();
	});

	// element references
	let container: HTMLElement;
	let cardTop: HTMLDivElement;
	let cardBottom: HTMLDivElement;
	let cardToAnimate: HTMLDivElement;

	// using svelte-5 runes '$state'
	let flipCtx: gsap.Context | null = $state(null);

	function anim() {
		flipCtx = gsap.context(() => {
			// 1. Flip Step 1 - Save the initial state
			const state = Flip.getState(cardToAnimate, { props: 'transform' });

			// 2. Flip Step 2 - Make the DOM changes
			// append the card background to bottom card
			cardBottom.appendChild(cardToAnimate);

			// 3. Flip Step 3 - Call Flip.from() with the initial state
			// And inside the variables, we've defined the final state of the animation
			// I hope the reason for naming this method 'from()' is clear now
			const flip = Flip.from(state, {
				absolute: true,
				rotate: '-2.5deg',
				translateX: '-0.5rem'
			});

			// Trigger to run the Flip animation
			ScrollTrigger.create({
				trigger: container,
				endTrigger: cardBottom,
				// start the animation when the top of the 'container' is at the top of the viewport
				start: 'top top',
				// end the animation when the bottom of the 'cardBottom' is 80% in the viewport
				end: 'bottom 80%',
				scrub: true,
				animation: flip,
				onLeave: () => {
					cardToAnimate.classList.remove('card-at-top');
				}
			});
		});
	}

	onDestroy(() => {
		flipCtx?.kill();
	});
</script>

<section bind:this={container} class="p-4 pb-64 w-full" onscroll={anim}>
	<!-- top card -->
	<div bind:this={cardTop} class="w-96 relative card ring-2">
		<!-- (This 👇🏻 will be animated with gsap-Flip) -->
		<div
			bind:this={cardToAnimate}
			data-explaining-class="We add both 'card-at-top' and 'card-at-bottom' classes because
				if we don't add the 'card-at-bottom' class, it gets tree shaken and never makes it to the final bundle.
				Inside the 'onLeave' callback, we remove the 'card-at-top' class when card reaches the bottom and then 'card-at-bottom' class becomes active.
				"
			class="card-to-animate card-at-top card-at-bottom bg-primary"
		></div>

		<div class="card-body z-10">
			<p class="text-sm text-primary-content font-semibold">
				Lorem ipsum dolor sit amet consectetur adipisicing elit. Sint error maxime at velit a soluta
				labore necessitatibus quo molestias asperiores?
			</p>
		</div>
	</div>

	<!-- Just to add some gap between top and bottom card -->
	<div class="h-[200vh] opacity-0">spacer</div>

	<section class="w-full flex justify-end">
		<!-- bottom card -->
		<div bind:this={cardBottom} class="w-96 relative card ring-2">
			<div class="card-body z-10">
				<p class="text-sm text-primary-content font-medium">
					Lorem ipsum dolor sit amet consectetur, adipisicing elit. Exercitationem dicta hic veniam,
					mollitia ex, vero neque dolor laudantium cupiditate nobis magni, deleniti incidunt
					suscipit ea nesciunt eligendi ipsum autem! Dolorum nostrum assumenda alias, magni ullam
					quisquam tenetur itaque. Illum officia cupiditate tenetur itaque, id ea qui suscipit
					nesciunt rerum nostrum.
				</p>
			</div>
		</div>
	</section>
</section>

<style>
	.card-to-animate {
		@apply absolute w-full h-full rounded-box border-4 border-base-content;
		left: 0;
		top: 0;

		/* The order of classes below is important, first we write 'card-at-bottom' and then 'card-at-top' */
		&.card-at-bottom {
			transform: rotate(-2.5deg) translateX(-0.5rem);
		}

		&.card-at-top {
			transform: rotate(2.5deg) translateX(0.5rem);
		}
	}
</style>
