<script lang="ts">
	interface Props {
		maxWidth?: 'xs' | 'sm' | 'md' | 'lg' | 'xl' | '2xl' | '3xl' | '4xl' | '5xl' | '6xl' | '7xl' | 'full';
		centered?: boolean;
		fluid?: boolean;
		class?: string;
		children?: any;
	}

	let {
		maxWidth = 'lg',
		centered = true,
		fluid = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'container';
		
		if (!fluid && maxWidth !== 'full') result += ` max-w-${maxWidth}`;
		if (centered) result += ' mx-auto';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>