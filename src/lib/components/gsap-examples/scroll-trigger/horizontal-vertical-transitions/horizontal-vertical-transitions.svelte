<script lang="ts">
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/dist/ScrollTrigger';
	import { onMount } from 'svelte';

	let currentIndex = $state(0);
	let isAnimating = $state(false);
	let scrollSection: HTMLElement;
	let scrollSectionChildren: HTMLElement[] = $state([]);
	let observer: Observer;

	onMount(() => {
		console.clear();

		gsap.registerPlugin(ScrollTrigger);

		scrollSectionChildren = gsap.utils.toArray(document.querySelectorAll('[data-swipe-panel]'));

		gsap.set(
			scrollSectionChildren.slice(1), // skip the first panel since it's already in view
			{
				xPercent: 100 // move all panels to the right except the first panel
			}
		);

		gsap.set(scrollSectionChildren, {
			zIndex: (i) => i // set z-indexes so that the panels are stacked on top of each other
		});

		/* 
		  We save this observer in a state so we can disable it when we reach the last panel
			and we enable it back again using the observer below this one.
			Property `preventDefault: true` prevents the vertical scrolling of the scroll container, but when we reach the last panel
			this observer should be disabled for scrolling to work again.
		*/
		observer = ScrollTrigger.observe({
			target: scrollSection,
			type: 'wheel,touch',
			tolerance: 10,
			preventDefault: true,
			onPress: (self) => {
				ScrollTrigger.isTouch && self.event.preventDefault();
			},
			onUp: (self) => {
				// only animate if not already animating
				if (!isAnimating && self.scrollY() === 0) gotoPanel(currentIndex - 1, false);
			},
			onDown: (self) => {
				if (!isAnimating && self.scrollY() === 0) gotoPanel(currentIndex + 1, true);
			}
		});

		/* 
			This observer is used to re-enable the `observer` above
			when we reach the top of the last panel and scroll up one more time.
			Because that is when `onUp` event is triggered and we can re-enable the observer.
		*/
		ScrollTrigger.observe({
			target: scrollSection,
			onUp: (self) => {
				// only enable the observer when we reach the top of the last panel and scroll up one more time
				if (
					!isAnimating &&
					currentIndex === scrollSectionChildren.length - 1 &&
					self.scrollY() === 0
				) {
					gotoPanel(currentIndex - 1, false);
					observer.enable();
				}
			}
		});
	});

	function gotoPanel(newIndex: number, isScrollingDown: boolean) {
		if (newIndex < 0 || newIndex > scrollSectionChildren.length - 1) return;

		// disable the observer when we reach the last panel to enable vertical scrolling
		if (newIndex === scrollSectionChildren.length - 1) {
			observer.disable();
		}

		isAnimating = true;

		// if scrolling down then new index is the current index + 1
		// if scrolling up then new index is the current index - 1 which is the currentIndex itself
		const target = isScrollingDown
			? scrollSectionChildren[newIndex]
			: scrollSectionChildren[currentIndex];

		gsap.to(target, {
			xPercent: isScrollingDown ? 0 : 100, // because in the beginning we set all panels to 100% to the right
			duration: 0.4,
			onComplete: () => {
				isAnimating = false;
			}
		});

		// update the current index
		currentIndex = newIndex;
	}
</script>

<section class="w-full max-w-3xl h-[50vh] border-2 rounded-box overflow-scroll">
	<section
		bind:this={scrollSection}
		class={`relative w-full h-full ${currentIndex === scrollSectionChildren.length - 1 ? 'overflow-x-hidden' : 'overflow-hidden'}`}
	>
		<div data-swipe-panel class="absolute w-full h-[50vh] bg-rose-800 center-text">Index 0</div>
		<div data-swipe-panel class="absolute w-full h-[50vh] bg-sky-800 center-text">Index 1</div>
		<div data-swipe-panel class="absolute w-full h-[50vh] bg-purple-800 center-text">Index 2</div>
		<div data-swipe-panel class="absolute w-full h-[300vh] bg-teal-800 center-text">
			<span class="absolute top-[4%] left-[12%] animate-bounce">Scroll Down</span>
			Index 3
		</div>
	</section>
</section>

<style>
	.center-text {
		@apply flex items-center justify-center text-8xl font-bold;
	}
</style>
