<script lang="ts">
	import gsap from 'gsap';
	import Observer from 'gsap/dist/Observer';
	import ScrollTrigger from 'gsap/dist/ScrollTrigger';

	import { onMount } from 'svelte';

	let container: HTMLElement;
	let scrollTo: gsap.QuickToFunc | undefined = $state();
	let startScroll: Number | undefined = $state(0);

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger, Observer);

		const panelContainer = document.querySelector('[data-panel-container]');
		const panels = gsap.utils.toArray(document.querySelectorAll('[data-panel]')) as HTMLElement[];

		gsap.to(panels, {
			xPercent: -100 * (panels.length - 1), // slide all panels to the left
			ease: 'none', // Important: this is what locks the panels to the scroll bar
			scrollTrigger: {
				trigger: panelContainer,
				pin: true,
				end: '+=1000%', // this sort of determines the scroll speed
				scrub: 0.3,
				scroller: container // if not set, then the viewport is used
			}
		});
	});
</script>

<section
	bind:this={container}
	class="w-full h-[700px] bg-black overflow-y-scroll overflow-x-hidden rounded-2xl ring-4 ring-black"
>
	<!-- First Vertical Scroll Section -->
	<section class={`px-5 py-44 w-full flex flex-col items-center gap-y-6 text-center bg-red-800`}>
		<h3 class="font-black">First Vertical Scroll Section</h3>
		<p class="text-xl max-w-lg">
			Lorem ipsum, dolor sit amet consectetur adipisicing elit. Nihil doloribus omnis placeat nulla
			voluptate corrupti ipsam magnam, tenetur vero hic deserunt commodi nemo voluptates molestias
			dignissimos nobis velit quisquam sunt possimus, ab, veritatis consequuntur at. Facilis natus
			ipsum non velit sapiente itaque eligendi, distinctio nesciunt accusamus, et maiores odio ullam
			recusandae iste beatae numquam? Libero temporibus rerum natus totam quae assumenda possimus!
			Aliquid error at voluptatum quae nostrum veritatis ab eos, totam delectus perferendis
			consequuntur! Error maiores aut reprehenderit libero nesciunt dolore corrupti pariatur aliquid
			temporibus voluptatibus esse provident corporis, velit amet consequatur exercitationem
			incidunt tenetur dolor placeat minus quo.
		</p>
	</section>

	<section
		data-panel-container
		class={`w-[500%] h-[700px] flex flex-nowrap text-center font-black`}
	>
		<div data-panel class={`py-20 w-full bg-sky-800`}>Panel 1</div>
		<div data-panel class={`py-20 w-full bg-teal-800`}>Panel 2</div>
		<div data-panel class={`py-20 w-full bg-purple-800`}>Panel 3</div>
		<div data-panel class={`py-20 w-full bg-pink-800`}>Panel 4</div>
		<div data-panel class={`py-20 w-full bg-green-800`}>Panel 5</div>
	</section>

	<!-- Last Vertical Scroll Section -->
	<section class={`px-5 py-44 w-full flex flex-col items-center gap-y-6 text-center bg-amber-800`}>
		<h3 class="font-black">Last Vertical Scroll Section</h3>
		<p class="text-xl max-w-lg">
			Lorem ipsum dolor, sit amet consectetur adipisicing elit. Eos non odit maiores incidunt.
			Placeat amet doloribus incidunt, nihil itaque, quisquam eius dolores molestiae exercitationem,
			a quis possimus nam aperiam! Doloribus error natus fuga, inventore rem hic ipsum? Delectus
			totam, voluptas inventore dignissimos vel error sint voluptatem numquam in rem sunt blanditiis
			ipsa ab, sequi autem quos asperiores velit sapiente molestiae, aperiam aspernatur eveniet.
			Rerum quis ducimus illum, ex earum, quidem asperiores et odit vero iusto id sequi doloribus
			officiis! Quaerat cumque repellat id alias odit, ullam voluptates, sapiente maiores commodi,
			facilis magnam nemo in tempora atque enim repellendus. Aliquid, molestiae.
		</p>
	</section>
</section>
