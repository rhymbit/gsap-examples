<script lang="ts">
	import NavbarDropdown from './navbar-dropdown.svelte';
</script>

<div class="navbar bg-primary/20">
	<div class="navbar-start">
		<a href="/" class="btn btn-ghost text-xl">GSAP Examples</a>
	</div>
	<div class="navbar-center flex">
		<ul class="menu menu-horizontal px-1">
			<li>
				<NavbarDropdown
					buttonTitle="Flip"
					items={[
						{ label: 'Cards Slider', href: 'cards-slider' },
						{ label: 'Card Sweeping With Scrollbar', href: 'card-sweeping-with-scrollbar' }
					]}
				/>
			</li>
		</ul>
	</div>
	<div class="navbar-end"></div>
</div>
