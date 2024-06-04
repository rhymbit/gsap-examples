<script lang="ts">
	/**
	 * Inspired from - https://codepen.io/GreenSock/pen/poaPzgp
	 * Uses GSAP Flip plugin to animate the expanding input
	 */

	import gsap from 'gsap';
	import { Flip } from 'gsap/Flip';
	import { onMount } from 'svelte';

	onMount(() => {
		gsap.registerPlugin(Flip);
	});

	function onkeyup(e: KeyboardEvent & { currentTarget: EventTarget & HTMLInputElement }) {
		// save the state
		const state = Flip.getState('#inputWide');

		// make dom changes
		const textLength = e.currentTarget.value.length;
		if (textLength > 0) {
			e.currentTarget.classList.add('input-wider');
		} else {
			e.currentTarget.classList.remove('input-wider');
		}

		// call Flip.from()
		Flip.from(state);
	}
</script>

<section>
	<input id="inputWide" type="text" class={`input input-lg input-accent`} {onkeyup} />
</section>

<style>
	.input-wider {
		width: 70vw;
	}
</style>
