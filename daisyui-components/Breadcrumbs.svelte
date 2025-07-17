<script lang="ts">
	interface BreadcrumbItem {
		label: string;
		href?: string;
		icon?: any;
		active?: boolean;
	}

	interface Props {
		items: BreadcrumbItem[];
		maxWidth?: string;
		class?: string;
	}

	let {
		items,
		maxWidth,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'breadcrumbs';
		
		if (className) result += ` ${className}`;
		
		return result;
	});

	let containerStyle = $derived(() => {
		if (maxWidth) return `max-width: ${maxWidth}`;
		return undefined;
	});
</script>

<div class={classes()} style={containerStyle} {...restProps}>
	<ul>
		{#each items as item, index}
			<li>
				{#if item.href && !item.active}
					<a href={item.href}>
						{#if item.icon}
							{@render item.icon()}
						{/if}
						{item.label}
					</a>
				{:else}
					<span>
						{#if item.icon}
							{@render item.icon()}
						{/if}
						{item.label}
					</span>
				{/if}
			</li>
		{/each}
	</ul>
</div>