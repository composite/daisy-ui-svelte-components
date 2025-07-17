<script lang="ts">
	interface Props {
		variant?: 'squircle' | 'heart' | 'hexagon' | 'hexagon-2' | 'decagon' | 'pentagon' | 'diamond' | 'square' | 'circle' | 'star' | 'star-2' | 'triangle' | 'triangle-2' | 'triangle-3' | 'triangle-4' | 'half-1' | 'half-2';
		class?: string;
		children?: any;
	}

	let {
		variant,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'mask';
		
		if (variant) result += ` mask-${variant}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>
