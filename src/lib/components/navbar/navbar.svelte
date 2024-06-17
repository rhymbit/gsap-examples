<script lang="ts">
	import NavbarDropdown from './navbar-dropdown.svelte';
</script>

<div class="navbar bg-base-300">
	<div class="navbar-start">
		<a href="/" class="btn btn-ghost text-xl">GSAP Examples</a>
	</div>
	<div class="navbar-center flex">
		<ul class="menu menu-horizontal px-1">
			<li>
				<a href="/attention-grab-text">Attention Grab Text</a>
			</li>
			<li>
				<NavbarDropdown
					buttonTitle="Flip"
					items={[
						{ label: 'Cards Slider', href: '/flip/cards-slider' },
						{ label: 'Elements Swap', href: '/flip/elements-swap' },
						{ label: 'Tarot Cards', href: '/flip/tarot-cards' },
						{ label: 'Expanding Input', href: '/flip/expanding-input' },
						{ label: 'Expanding Item', href: '/flip/expanding-item' },
						{ label: 'Layout Change', href: '/flip/layout-change' },
						{ label: 'Photo Gallery', href: '/flip/photo-gallery' },
						{ label: 'Cassie Wheel', href: '/flip/cassie-wheel' },
						{ label: 'Card Sweeping With Scrollbar', href: '/flip/card-sweeping-with-scrollbar' },
						{ label: 'Move Items Between Containers', href: '/flip/move-items-btw-containers' }
					]}
				/>
			</li>
			<li>
				<NavbarDropdown
					buttonTitle="Scroll Trigger"
					items={[
						{
							label: 'Horizontal Vertical Transitions',
							href: '/scroll-trigger/horizontal-vertical-transitions'
						},
						{
							label: 'Vertical Horizontal Transitions',
							href: '/scroll-trigger/vertical-horizontal-transitions'
						}
					]}
				/>
			</li>
		</ul>
	</div>
	<div class="navbar-end"></div>
</div>
