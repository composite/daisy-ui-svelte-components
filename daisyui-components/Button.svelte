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
		
		if (variant) result += ` btn-${variant}`;
		if (size) result += ` btn-${size}`;
		if (style) result += ` btn-${style}`;
		if (shape) result += ` btn-${shape}`;
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

