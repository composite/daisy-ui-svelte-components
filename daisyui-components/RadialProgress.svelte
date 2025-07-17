<script lang="ts">
	interface Props {
		value: number;
		size?: string;
		thickness?: string;
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		class?: string;
		children?: any;
	}

	let {
		value,
		size = '4rem',
		thickness = '2px',
		color,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'radial-progress';
		
		if (color) result += ` text-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});

	let style = $derived(() => {
		return `--value:${value}; --size:${size}; --thickness:${thickness};`;
	});
</script>

<div 
	class={classes()} 
	{style}
	role="progressbar"
	aria-valuenow={value}
	aria-valuemin="0"
	aria-valuemax="100"
	{...restProps}
>
	{#if children}
		{@render children()}
	{:else}
		{value}%
	{/if}
</div>