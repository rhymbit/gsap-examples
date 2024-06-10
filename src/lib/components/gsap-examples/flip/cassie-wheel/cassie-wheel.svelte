<script lang="ts">
	/**
	 * Inspired from Cassie Evans - https://codepen.io/cassie-codes/pen/abyZYym
	 */
	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import ScrollTrigger from 'gsap/dist/ScrollTrigger';
	import image1 from './assets/image-1.jpg';
	import image10 from './assets/image-10.jpg';
	import image11 from './assets/image-11.jpg';
	import image12 from './assets/image-12.jpg';
	import image13 from './assets/image-13.jpg';
	import image14 from './assets/image-14.jpg';
	import image15 from './assets/image-15.jpg';
	import image16 from './assets/image-16.jpg';
	import image17 from './assets/image-17.jpg';
	import image18 from './assets/image-18.jpg';
	import image19 from './assets/image-19.jpg';
	import image2 from './assets/image-2.jpg';
	import image20 from './assets/image-20.jpg';
	import image21 from './assets/image-21.jpg';
	import image22 from './assets/image-22.jpg';
	import image23 from './assets/image-23.jpg';
	import image24 from './assets/image-24.jpg';
	import image25 from './assets/image-25.jpg';
	import image26 from './assets/image-26.jpg';
	import image27 from './assets/image-27.jpg';
	import image28 from './assets/image-28.jpg';
	import image3 from './assets/image-3.jpg';
	import image4 from './assets/image-4.jpg';
	import image5 from './assets/image-5.jpg';
	import image6 from './assets/image-6.jpg';
	import image7 from './assets/image-7.jpg';
	import image8 from './assets/image-8.jpg';
	import image9 from './assets/image-9.jpg';

	const images = [
		image1,
		image2,
		image3,
		image4,
		image5,
		image6,
		image7,
		image8,
		image9,
		image10,
		image11,
		image12,
		image13,
		image14,
		image15,
		image16,
		image17,
		image18,
		image19,
		image20,
		image21,
		image22,
		image23,
		image24,
		image25,
		image26,
		image27,
		image28
	];

	$effect(() => {
		gsap.registerPlugin(Flip, ScrollTrigger);
		setup();

		gsap.to(wheel, {
			rotate: () => -360,
			ease: 'none',
			duration: images.length,
			scrollTrigger: {
				start: 0,
				end: 'max',
				scrub: 1,
				snap: 1 / images.length,
				invalidateOnRefresh: true
			}
		});
	});

	let wheel: HTMLElement;

	function setup() {
		let radius = wheel.offsetWidth / 2;
		let center = wheel.offsetWidth / 2;
		let slice = (2 * Math.PI) / images.length;

		const wheelImages = wheel.querySelectorAll('[data-wheel-image]');

		gsap.utils.toArray(wheelImages).forEach((item, i) => {
			let angle = i * slice;

			// angles are calculated normally. We add `center` to x and y to center the wheel properly.
			let x = radius * Math.sin(angle) + center;
			let y = -(radius * Math.cos(angle)) + center;

			gsap.set(item as HTMLImageElement, {
				rotation: angle + '_rad',
				xPercent: -50,
				yPercent: -50,
				x: x,
				y: y
			});
		});
	}
</script>

<svelte:window onresize={setup} />

<section class="w-[100vw] h-[600vh]">
	<section class="w-full h-[22vh] fixed bottom-[10%]">
		<section
			bind:this={wheel}
			class={`absolute top-0 left-1/2 -translate-x-[50%] w-[300vw] h-[300vh] max-w-[2000px] max-h-[2000px] flex items-center justify-center`}
		>
			{#each images as image}
				<div data-wheel-image class="absolute top-0 left-0 w-[7%] max-w-[200px] aspect-square">
					<img
						src={image}
						alt=""
						class="w-full pointer-events-none z-[999] rounded-box shadow-xl shadow-secondary"
					/>
				</div>
			{/each}
		</section>
	</section>
</section>
