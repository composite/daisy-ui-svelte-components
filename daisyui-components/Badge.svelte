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
		
		// Variant classes
		if (variant === 'neutral') result += ' badge-neutral';
		if (variant === 'primary') result += ' badge-primary';
		if (variant === 'secondary') result += ' badge-secondary';
		if (variant === 'accent') result += ' badge-accent';
		if (variant === 'info') result += ' badge-info';
		if (variant === 'success') result += ' badge-success';
		if (variant === 'warning') result += ' badge-warning';
		if (variant === 'error') result += ' badge-error';
		if (variant === 'ghost') result += ' badge-ghost';
		
		// Size classes
		if (size === 'xs') result += ' badge-xs';
		if (size === 'sm') result += ' badge-sm';
		if (size === 'md') result += ' badge-md';
		if (size === 'lg') result += ' badge-lg';
		if (size === 'xl') result += ' badge-xl';
		
		// Style classes
		if (style === 'outline') result += ' badge-outline';
		if (style === 'dash') result += ' badge-dash';
		if (style === 'soft') result += ' badge-soft';
		
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<span class={classes()} {...restProps}>
	{@render children?.()}
</span>
