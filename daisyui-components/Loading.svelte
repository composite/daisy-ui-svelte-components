<script lang="ts">
	interface Props {
		type?: 'spinner' | 'dots' | 'ring' | 'ball' | 'bars' | 'infinity';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		class?: string;
	}

	let {
		type = 'spinner',
		size,
		color,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'loading';
		
		if (type) result += ` loading-${type}`;
		if (size) result += ` loading-${size}`;
		if (color) result += ` text-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<span class={classes()} {...restProps}></span>