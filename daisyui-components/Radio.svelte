<script lang="ts">
	interface Props {
		name: string;
		value: string | number;
		checked?: boolean;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		disabled?: boolean;
		required?: boolean;
		class?: string;
	}

	let {
		name,
		value,
		checked = $bindable(),
		size,
		color,
		disabled = false,
		required = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'radio';
		
		if (size) result += ` radio-${size}`;
		if (color) result += ` radio-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<input
	type="radio"
	{name}
	{value}
	checked={checked}
	{disabled}
	{required}
	class={classes()}
	{...restProps}
/>