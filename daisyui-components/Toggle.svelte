<script lang="ts">
	interface Props {
		checked?: boolean;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		disabled?: boolean;
		indeterminate?: boolean;
		class?: string;
	}

	let {
		checked = $bindable(),
		size,
		color,
		disabled = false,
		indeterminate = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'toggle';
		
		if (size) result += ` toggle-${size}`;
		if (color) result += ` toggle-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<input
	type="checkbox"
	bind:checked
	{disabled}
	{indeterminate}
	class={classes()}
	{...restProps}
/>