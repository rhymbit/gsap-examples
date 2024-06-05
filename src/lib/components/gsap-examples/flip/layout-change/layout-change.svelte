<script lang="ts">
	/**
	 * Inspired from - https://codepen.io/GreenSock/pen/eYdyVVe
	 * Uses GSAP's Flip plugin to animate layout changes
	 */

	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import { onMount, tick } from 'svelte';
	import TextPlugin from 'gsap/dist/TextPlugin';
	/**
	 * Checkout the css file for the classes used in this component
	 */
	import './layout-change.css';

	onMount(() => {
		// register the plugin 'Flip', and
		// 'TextPlugin' is just used to animate current layout text and is not the main part of the animation
		gsap.registerPlugin(Flip, TextPlugin);
		// start the animation, 'delayedCall' is like gsap's setTimeout
		gsap.delayedCall(1, nextState);
	});

	// four layouts to cycle through
	const layouts = ['final', 'plain', 'columns', 'grid'];
	let currentLayoutIndex = $state(0);
	// element references
	let container: HTMLElement;
	let currentLayoutText: HTMLElement;

	// effect to update the current layout text, not part of the main animation
	$effect(() => {
		gsap.to(currentLayoutText, {
			duration: 0.6,
			text: layouts[currentLayoutIndex]
		});
	});

	async function nextState() {
		// (1). Save the state for stuff to be animated
		const state = Flip.getState('.letter, .for, .gsap', {
			simple: true
		});

		// (2). Make DOM Changes - remove the current layout class and add the next layout class
		container.classList.remove(layouts[currentLayoutIndex]);
		currentLayoutIndex = (currentLayoutIndex + 1) % layouts.length;
		await tick();
		container.classList.add(layouts[currentLayoutIndex]);

		// (3). Call Flip.from() to animate the changes
		Flip.from(state, {
			absolute: true,
			stagger: 0.07,
			duration: 0.7,
			ease: 'power2.inOut',
			spin: currentLayoutIndex === 0, // only spin when going to the "final" layout
			simple: true, // with simple:true, GSAP's Flip plugin animates efficiently because it doesn't have to calculate the position of each element
			/**
			 * 'onEnter' and 'onLeave' are used for text 'for' & 'gsap'
			 * to animate their opacity when they enter and leave the DOM
			 */
			onEnter: (elements) => {
				return gsap.from(elements, { opacity: 0, delay: 0.8 });
			},
			onLeave: (elements) => {
				gsap.to(elements, { opacity: 0 });
			}
		});

		// (4). Call nextState() again
		gsap.delayedCall(currentLayoutIndex === 0 ? 2.5 : 1.5, nextState);
	}
</script>

<!-- This 👇🏻 text is just to show the current animating layout -->
<section bind:this={currentLayoutText} class="flex justify-center underline-offset-4">
	{layouts[currentLayoutIndex]}
</section>

<section bind:this={container} class="container final">
	<div class="letter bg-teal-700">F</div>
	<div class="letter bg-amber-700">L</div>
	<div class="letter bg-sky-700">I</div>
	<div class="letter bg-rose-700">P</div>
	<div class="for">for</div>
	<div class="gsap">GSAP</div>
</section>

<style>
</style>
