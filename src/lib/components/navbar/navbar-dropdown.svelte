<script lang="ts">
	type Props = {
		buttonTitle: string;
		items: { label: string; href: string }[];
	};

	const { buttonTitle = '', items = [] }: Props = $props();
</script>

<div class="dropdown dropdown-bottom dropdown-hover">
	<div tabindex="0" role="button">{buttonTitle}</div>
	<ul
		class="dropdown-content w-max max-w-xs pt-4
		relative before:absolute before:inset-0 before:w-full before:h-full before:mt-4 before:pr-3 before:bg-base-300 before:opacity-100
		before:rounded-b-box
		"
	>
		{#each items as { label, href }}
			<li>
				<a {href}>
					{label}
				</a>
			</li>
		{/each}
	</ul>
</div>
