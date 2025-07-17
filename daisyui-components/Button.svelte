<script lang="ts">
	interface Props {
		variant?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error' | 'ghost' | 'link';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		style?: 'outline' | 'dash' | 'soft';
		shape?: 'square' | 'circle';
		disabled?: boolean;
		loading?: boolean;
		wide?: boolean;
		block?: boolean;
		active?: boolean;
		href?: string;
		type?: 'button' | 'submit' | 'reset';
		class?: string;
		children?: any;
		onclick?: () => void;
	}

	let {
		variant = 'neutral',
		size,
		style,
		shape,
		disabled = false,
		loading = false,
		wide = false,
		block = false,
		active = false,
		href,
		type = 'button',
		class: className,
		children,
		onclick,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'btn';
		
		// Variant classes
		if (variant === 'neutral') result += ' btn-neutral';
		if (variant === 'primary') result += ' btn-primary';
		if (variant === 'secondary') result += ' btn-secondary';
		if (variant === 'accent') result += ' btn-accent';
		if (variant === 'info') result += ' btn-info';
		if (variant === 'success') result += ' btn-success';
		if (variant === 'warning') result += ' btn-warning';
		if (variant === 'error') result += ' btn-error';
		if (variant === 'ghost') result += ' btn-ghost';
		if (variant === 'link') result += ' btn-link';
		
		// Size classes
		if (size === 'xs') result += ' btn-xs';
		if (size === 'sm') result += ' btn-sm';
		if (size === 'md') result += ' btn-md';
		if (size === 'lg') result += ' btn-lg';
		if (size === 'xl') result += ' btn-xl';
		
		// Style classes
		if (style === 'outline') result += ' btn-outline';
		if (style === 'dash') result += ' btn-dash';
		if (style === 'soft') result += ' btn-soft';
		
		// Shape classes
		if (shape === 'square') result += ' btn-square';
		if (shape === 'circle') result += ' btn-circle';
		
		// State classes
		if (wide) result += ' btn-wide';
		if (block) result += ' btn-block';
		if (active) result += ' btn-active';
		if (disabled) result += ' btn-disabled';
		
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

{#if href}
	<a {href} class={classes()} {...restProps}>
		{#if loading}
			<span class="loading loading-spinner"></span>
		{/if}
		{@render children?.()}
	</a>
{:else}
	<button {type} class={classes()} disabled={disabled || loading} {onclick} {...restProps}>
		{#if loading}
			<span class="loading loading-spinner"></span>
		{/if}
		{@render children?.()}
	</button>
{/if}

