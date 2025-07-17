<script lang="ts">
	interface Props {
		width?: string;
		height?: string;
		shape?: 'rectangle' | 'circle';
		class?: string;
	}

	let {
		width = 'w-full',
		height = 'h-4',
		shape = 'rectangle',
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'skeleton';
		
		result += ` ${width} ${height}`;
		
		if (shape === 'circle') result += ' rounded-full';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}></div>