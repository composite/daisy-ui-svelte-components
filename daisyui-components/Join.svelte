<script lang="ts">
	interface Props {
		direction?: 'horizontal' | 'vertical';
		class?: string;
		children?: any;
	}

	let {
		direction = 'horizontal',
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'join';
		
		if (direction === 'vertical') result += ' join-vertical';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>
