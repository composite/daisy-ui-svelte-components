<script lang="ts">
	interface Props {
		min?: number;
		max?: number;
		step?: number;
		value?: number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		disabled?: boolean;
		class?: string;
	}

	let {
		min = 0,
		max = 100,
		step = 1,
		value = $bindable(),
		size,
		color,
		disabled = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'range';
		
		if (size) result += ` range-${size}`;
		if (color) result += ` range-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<input
	type="range"
	{min}
	{max}
	{step}
	bind:value
	{disabled}
	class={classes()}
	{...restProps}
/>