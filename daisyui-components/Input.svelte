<script lang="ts">
	interface Props {
		type?: 'text' | 'email' | 'password' | 'number' | 'tel' | 'url' | 'search';
		placeholder?: string;
		value?: string | number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		ghost?: boolean;
		disabled?: boolean;
		required?: boolean;
		class?: string;
	}

	let {
		type = 'text',
		placeholder,
		value = $bindable(),
		size,
		color,
		ghost = false,
		disabled = false,
		required = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'input';
		
		if (ghost) result += ' input-ghost';
		if (size) result += ` input-${size}`;
		if (color) result += ` input-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<input
	{type}
	{placeholder}
	bind:value
	{disabled}
	{required}
	class={classes()}
	{...restProps}
/>