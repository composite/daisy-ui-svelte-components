<script lang="ts">
	interface Props {
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		direction?: 'horizontal' | 'vertical';
		class?: string;
		children?: any;
	}

	let {
		size,
		direction = 'vertical',
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'menu';
		
		if (size) result += ` menu-${size}`;
		if (direction === 'horizontal') result += ' menu-horizontal';
		else result += ' menu-vertical';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<ul class={classes()} {...restProps}>
	{@render children?.()}
</ul>
