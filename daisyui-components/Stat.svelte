<script lang="ts">
	interface Props {
		title?: string;
		value?: string | number;
		desc?: string;
		figure?: any;
		actions?: any;
		direction?: 'horizontal' | 'vertical';
		class?: string;
		children?: any;
	}

	let {
		title,
		value,
		desc,
		figure,
		actions,
		direction = 'vertical',
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'stat';

		if (className) result += ` ${className}`;

		return result;
	});

	let containerClasses = $derived(() => {
		let result = 'stats';

		if (direction === 'vertical') result += ' stats-vertical';
		if (direction === 'horizontal') result += ' stats-horizontal';

		return result;
	});
</script>

{#if children}
	<div class={containerClasses()} {...restProps}>
		{@render children()}
	</div>
{:else}
	<div class={classes()} {...restProps}>
		{#if figure}
			<div class="stat-figure">
				{@render figure()}
			</div>
		{/if}
		{#if title}
			<div class="stat-title">{title}</div>
		{/if}
		{#if value}
			<div class="stat-value">{value}</div>
		{/if}
		{#if desc}
			<div class="stat-desc">{desc}</div>
		{/if}
		{#if actions}
			<div class="stat-actions">
				{@render actions()}
			</div>
		{/if}
	</div>
{/if}
