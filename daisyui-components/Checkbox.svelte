<script lang="ts">
	interface Props {
		checked?: boolean;
		variant?: 'primary' | 'secondary' | 'accent' | 'neutral' | 'info' | 'success' | 'warning' | 'error';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		disabled?: boolean;
		indeterminate?: boolean;
		class?: string;
		onchange?: (checked: boolean) => void;
	}

	let {
		checked = $bindable(false),
		variant,
		size,
		disabled = false,
		indeterminate = false,
		class: className,
		onchange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'checkbox';
		
		if (variant) result += ` checkbox-${variant}`;
		if (size) result += ` checkbox-${size}`;
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleChange() {
		onchange?.(checked);
	}
</script>

<input 
	type="checkbox" 
	bind:checked 
	{disabled}
	{indeterminate}
	class={classes()} 
	onchange={handleChange}
	{...restProps} 
/>
