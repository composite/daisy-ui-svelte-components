<script lang="ts">
	interface Props {
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		style?: 'border' | 'dash';
		side?: boolean;
		imageFull?: boolean;
		glass?: boolean;
		class?: string;
		children?: any;
	}

	let {
		size,
		style,
		side = false,
		imageFull = false,
		glass = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'card';
		
		if (size) result += ` card-${size}`;
		if (style) result += ` card-${style}`;
		if (side) result += ' card-side';
		if (imageFull) result += ' image-full';
		if (glass) result += ' glass';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>
