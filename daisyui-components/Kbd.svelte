<script lang="ts">
	interface Props {
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		class?: string;
		children?: any;
	}

	let {
		size,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'kbd';
		
		if (size) result += ` kbd-${size}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<kbd class={classes()} {...restProps}>
	{@render children?.()}
</kbd>
