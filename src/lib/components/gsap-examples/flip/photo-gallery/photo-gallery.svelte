<script lang="ts">
	import gsap from 'gsap';
	import Flip from 'gsap/dist/Flip';
	/** Images sourced from unsplash */
	import photo1 from './assets/photo-1.webp';
	import photo2 from './assets/photo-2.webp';
	import photo3 from './assets/photo-3.webp';
	import photo4 from './assets/photo-4.webp';
	import photo5 from './assets/photo-5.webp';
	import photo6 from './assets/photo-6.webp';
	import { tick } from 'svelte';

	const photos = [photo1, photo2, photo3, photo4, photo5, photo6];

	let activeItem: HTMLElement | null = $state(null);
	let details: HTMLElement;
	let detailsContent: HTMLElement;
	let detailsImage: HTMLImageElement;
	let photosContainer: HTMLElement;

	$effect(() => {
		gsap.registerPlugin(Flip);

		detailsContent && gsap.set(detailsContent, { yPercent: -100 });
	});

	async function showDetail(e: MouseEvent & { currentTarget: HTMLImageElement }) {
		const item = e.currentTarget;

		if (item == activeItem) {
			await hideDetail();
			return;
		}

		function onImageLoad() {
			Flip.fit(details, item, { scale: true, fitChild: detailsImage });

			const state = Flip.getState(details);

			gsap.set(details, { clearProps: true });
			gsap.set(details, {
				xPercent: -50,
				top: '50%',
				yPercent: -50,
				visibility: 'visible'
			});

			Flip.from(state, {
				duration: 0.5,
				ease: 'power2.inOut',
				scale: true
			}).to(detailsContent, { yPercent: 0, duration: 0.2 });

			detailsImage.removeEventListener('load', onImageLoad);
			document.addEventListener('click', hideDetail);
		}

		detailsImage.addEventListener('load', onImageLoad);
		detailsImage.src = item.src;

		const items = gsap.utils.toArray(photosContainer.children);
		gsap
			.to(items, {
				opacity: 0.3,
				stagger: { amount: 0.7, from: items.indexOf(item), grid: 'auto' }
			})
			.kill(item);

		activeItem = item;
	}

	async function hideDetail() {
		document.removeEventListener('click', hideDetail);

		const state = Flip.getState(details);

		Flip.fit(details, activeItem, { scale: true, fitChild: detailsImage });

		const tl = gsap.timeline();

		const items = gsap.utils.toArray(photosContainer.children);

		tl.to(detailsContent, { yPercent: -100 }).to(items, {
			opacity: 1,
			stagger: { amount: 0.7, from: items.indexOf(activeItem), grid: 'auto' },
			duration: 0.2
		});

		Flip.from(state, {
			scale: true,
			duration: 0.5,
			delay: 0.25,
			onInterrupt: () => {
				tl.kill();
			}
		}).set(details, { visibility: 'hidden' });

		activeItem = null;
		await tick();
	}
</script>

<section>
	<section bind:this={photosContainer} class="p-4 max-w-6xl grid grid-cols-3 gap-2 bg-base-300">
		{#each photos as photo}
			<img
				src={photo}
				alt=""
				class={`w-full h-full rounded-box ring-2 ring-base-content cursor-pointer ${activeItem === null ? 'hover:scale-105 duration-300' : ''}`}
				data-title={photo?.split('/')?.pop()?.split('.')[0] ?? ''}
				onclick={activeItem === null ? showDetail : () => {}}
				role="none"
			/>
		{/each}
	</section>

	<section
		bind:this={details}
		class="fixed top-[10px] left-1/2 w-[90.1vmin] max-h-full flex flex-col invisible cursor-pointer overflow-auto"
	>
		<img bind:this={detailsImage} src="" alt="" class="z-[1] rounded-box border-2" />

		<div bind:this={detailsContent} class="px-3 py-2 bg-base-300 text-sm rounded-box">
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Temporibus nemo numquam nobis ab,
			ratione quis iusto corrupti modi cumque esse optio incidunt sed distinctio consectetur dicta
			illum voluptate. Unde ipsum veniam nesciunt beatae possimus est, quo totam rem. Optio corrupti
			excepturi quidem earum! Quidem aspernatur dolore quaerat iste. Quaerat, est.
		</div>
	</section>
</section>
