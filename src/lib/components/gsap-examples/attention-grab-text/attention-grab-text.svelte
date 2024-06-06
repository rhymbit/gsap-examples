<script lang="ts">
	/**
	 * Inspired from - https://codepen.io/GreenSock/pen/AYNVmv
	 * but uses a different approach to animate the text than what's shown in the codepen.
	 */

	import gsap from 'gsap';
	import { SlowMo } from 'gsap/dist/EasePack';
	import { onMount } from 'svelte';

	// text to animate
	const sampleText = `These words are constantly animating in your face to suck you in and leave you hanging for what comes next. Can you handle the awesomeness? Or are you left quivering in fear? It's only text, silly. Longer words stay on the screen for a greater duration. Each sentence ends with a dramatatic pause. Yes, that pause. The End`;

	// reference to the text container
	let textContainer: HTMLElement;

	onMount(() => {
		// register SlowMo ease plugin so we can use 'slow' ease
		gsap.registerPlugin(SlowMo);
		// call the animation function
		animateText(sampleText);
	});

	async function animateText(text: string) {
		let words = text.split(' ');

		// create a timeline
		let tl = gsap.timeline({
			delay: 0.6, // delay before the animation starts
			repeat: -1, // repeats infinitely
			repeatDelay: 2 // delay before the animation repeats
		});

		for (let i = 0; i < words.length; i++) {
			const word = words[i];

			// if it's an end word, we'll increase the duration of the animation
			const isSentenceEndWord = word.match(/[\.\?\!]/);

			// make dom changes - add a paragraph element for each word
			const paragraphElement = document.createElement('p');
			paragraphElement.textContent = word;
			paragraphElement.className = 'attention-grab-text';
			textContainer.appendChild(paragraphElement);

			let animationDuration = Math.max(0.5, word.length * 0.08);

			if (isSentenceEndWord) {
				animationDuration += 0.6;
			}

			// .set() is just like .to() but with a duration of 0
			tl.set(paragraphElement, {
				autoAlpha: 0,
				scale: 0.4,
				display: 'block', // initially word is hidden, also 'onComplete' below hid the word after the animation was completed
				z: 0.01 // set to 0.01 just to kick in 3D rendering and set off hardware acceleration which is needed for smooth animations
			}).fromTo(
				paragraphElement,
				{
					duration: animationDuration,
					scale: 0.8,
					ease: 'slow(0.25, 0.9)'
				},
				{
					duration: isSentenceEndWord ? animationDuration + 0.6 : animationDuration,
					autoAlpha: 1,
					scale: 1,
					ease: 'slow(0.25, 0.9, true)',
					onComplete: () => {
						paragraphElement.style.display = 'none'; // hide the word after the animation completes
					}
				}
			);
		}
	}
</script>

<section
	bind:this={textContainer}
	class="relative w-full max-w-4xl h-[400px] flex justify-center items-center bg-black rounded-box"
></section>

<style>
	:global(.attention-grab-text) {
		@apply hidden absolute font-black text-8xl;
		font-family: 'Roboto', sans-serif;
		font-size: 6rem;
		font-weight: 700;
		color: #fff;
		text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
	}
</style>
