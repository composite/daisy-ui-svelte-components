<script lang="ts">
	interface Props {
		variant?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error' | 'ghost';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		style?: 'outline' | 'dash' | 'soft';
		class?: string;
		children?: any;
	}

	let {
		variant = 'neutral',
		size,
		style,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'badge';
		
		if (variant) result += ` badge-${variant}`;
		if (size) result += ` badge-${size}`;
		if (style) result += ` badge-${style}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<span class={classes()} {...restProps}>
	{@render children?.()}
</span>
