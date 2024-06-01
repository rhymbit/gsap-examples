<script lang="ts">
	type Props = {
		buttonTitle: string;
		items: { label: string; href: string }[];
	};

	const { buttonTitle = '', items = [] }: Props = $props();
</script>

<div class="dropdown dropdown-bottom dropdown-hover">
	<div tabindex="0" role="button">{buttonTitle}</div>
	{#each items as { label, href }}
		<ul class="dropdown-content shadow w-max max-w-xs">
			<div class="p-2 mt-4 bg-primary/20 rounded-b-box">
				<li>
					<a {href}>
						{label}
					</a>
				</li>
			</div>
		</ul>
	{/each}
</div>
