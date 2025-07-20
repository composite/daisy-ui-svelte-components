<script lang="ts">
	interface Props {
		direction?: 'horizontal' | 'vertical';
		center?: boolean;
		class?: string;
		children?: any;
	}

	let {
		direction = 'vertical',
		center = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'footer';

		if (direction === 'horizontal') result += ' footer-horizontal';
		if (center) result += ' footer-center';
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<footer class={classes()} {...restProps}>
	{@render children?.()}
</footer>
