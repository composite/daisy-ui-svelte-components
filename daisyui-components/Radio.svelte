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
		
		// Size classes
		if (size === 'xs') result += ' radio-xs';
		if (size === 'sm') result += ' radio-sm';
		if (size === 'md') result += ' radio-md';
		if (size === 'lg') result += ' radio-lg';
		if (size === 'xl') result += ' radio-xl';
		
		// Color classes
		if (color === 'neutral') result += ' radio-neutral';
		if (color === 'primary') result += ' radio-primary';
		if (color === 'secondary') result += ' radio-secondary';
		if (color === 'accent') result += ' radio-accent';
		if (color === 'info') result += ' radio-info';
		if (color === 'success') result += ' radio-success';
		if (color === 'warning') result += ' radio-warning';
		if (color === 'error') result += ' radio-error';
		
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