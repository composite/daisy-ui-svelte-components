<script lang="ts">
	interface Props {
		icon?: 'arrow' | 'plus';
		open?: boolean;
		checkbox?: boolean;
		close?: boolean;
		class?: string;
		title?: any;
		children?: any;
	}

	let {
		icon,
		open = $bindable(false),
		checkbox = false,
		close = false,
		class: className,
		title,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'collapse';
		
		if (icon) result += ` collapse-${icon}`;
		if (open) result += ' collapse-open';
		if (close) result += ' collapse-close';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} tabindex="0" {...restProps}>
	{#if checkbox}
		<input type="checkbox" bind:checked={open} />
	{/if}
	<div class="collapse-title">
		{#if title}
			{@render title()}
		{/if}
	</div>
	<div class="collapse-content">
		{@render children?.()}
	</div>
</div>
