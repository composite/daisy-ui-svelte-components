<script lang="ts">
	interface Props {
		snap?: 'start' | 'center' | 'end';
		direction?: 'horizontal' | 'vertical';
		class?: string;
		children?: any;
	}

	let {
		snap,
		direction = 'horizontal',
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'carousel';
		
		if (snap) result += ` carousel-${snap}`;
		if (direction === 'vertical') result += ' carousel-vertical';
		else result += ' carousel-horizontal';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>
