<script lang="ts">
	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	import bananasPic from './assets/bananas.jpg';

	$effect(() => {
		gsap.registerPlugin(Flip);
	});

	let cardBg: HTMLElement;
	let cardBgState: Flip.FlipState | undefined = $state();
	let cardImage: HTMLImageElement;
	let cardImageState: Flip.FlipState | undefined = $state();

	let details: HTMLElement;
	let detailsBg: HTMLElement;
	let detailsImage: HTMLImageElement;

	function onCardClick() {
		cardBgState = Flip.getState(cardBg);
		cardImageState = Flip.getState(cardImage);

		Flip.fit(cardBg, detailsBg, {
			scale: true,
			duration: 0.8,
			ease: 'power2.out',
			backgroundColor: 'hsl(32, 81%, 29%)'
		});

		Flip.fit(cardImage, detailsImage, {
			scale: true,
			duration: 0.6,
			ease: 'bounce.out'
		});

		gsap.to(details, {
			duration: 1,
			visibility: 'visible',
			opacity: 1
		});
	}

	function onXClick() {
		if (!cardBgState || !cardImageState) return;

		Flip.fit(cardBg, cardBgState, {
			scale: true,
			duration: 0.4
		});

		Flip.fit(cardImage, cardImageState, {
			scale: true,
			duration: 0.4,
			ease: 'power2.out'
		});

		const tl = gsap.timeline();

		tl.to(details, {
			duration: 0.4,
			opacity: 0
		}).to(details, {
			duration: 0,
			visibility: 'hidden'
		});

		cardBgState = undefined;
	}
</script>

<div
	class={`relative w-[600px] flex justify-between item-center cursor-pointer`}
	onclick={onCardClick}
	role="none"
>
	<h1 class="w-full flex justify-center items-center text-4xl">Bananas</h1>
	<img bind:this={cardImage} src={bananasPic} alt="" class="max-w-xs w-full h-full" />
	<!-- card background -->
	<div bind:this={cardBg} class="-z-10 absolute w-full h-full bg-yellow-800"></div>
</div>

<section
	bind:this={details}
	class={`fixed bottom-0 w-full h-[50%] flex justify-between opacity-0 invisible`}
>
	<div class="px-14 py-20 max-w-5xl">
		<h1 class="text-6xl font-black">Banana</h1>
		<p class="text-xl">
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Temporibus corporis non beatae
			provident rem at officia optio id quia tempore.
		</p>
	</div>

	<div class={`relative -top-20 right-44`}>
		<img
			bind:this={detailsImage}
			src={bananasPic}
			alt=""
			class={`max-w-md rounded-box shadow-xl shadow-secondary invisible`}
		/>
	</div>

	<div bind:this={detailsBg} class="absolute -z-10 top-0 left-0 w-full h-full"></div>

	<div onclick={onXClick} role="none" class="absolute -top-3 right-10 cursor-pointer">x</div>
</section>
