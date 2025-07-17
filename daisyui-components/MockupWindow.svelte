<script lang="ts">
	interface Props {
		backgroundColor?: string;
		class?: string;
		children?: any;
	}

	let {
		backgroundColor,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'mockup-window';
		
		if (backgroundColor) result += ` ${backgroundColor}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>