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
		
		// Variant classes
		if (variant === 'primary') result += ' checkbox-primary';
		if (variant === 'secondary') result += ' checkbox-secondary';
		if (variant === 'accent') result += ' checkbox-accent';
		if (variant === 'neutral') result += ' checkbox-neutral';
		if (variant === 'info') result += ' checkbox-info';
		if (variant === 'success') result += ' checkbox-success';
		if (variant === 'warning') result += ' checkbox-warning';
		if (variant === 'error') result += ' checkbox-error';
		
		// Size classes
		if (size === 'xs') result += ' checkbox-xs';
		if (size === 'sm') result += ' checkbox-sm';
		if (size === 'md') result += ' checkbox-md';
		if (size === 'lg') result += ' checkbox-lg';
		if (size === 'xl') result += ' checkbox-xl';
		
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
