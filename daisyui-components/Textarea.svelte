<script lang="ts">
	interface Props {
		placeholder?: string;
		value?: string;
		rows?: number;
		cols?: number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		ghost?: boolean;
		disabled?: boolean;
		required?: boolean;
		resize?: boolean;
		class?: string;
	}

	let {
		placeholder,
		value = $bindable(),
		rows,
		cols,
		size,
		color,
		ghost = false,
		disabled = false,
		required = false,
		resize = true,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'textarea';
		
		if (ghost) result += ' textarea-ghost';
		if (size) result += ` textarea-${size}`;
		if (color) result += ` textarea-${color}`;
		if (!resize) result += ' resize-none';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<textarea
	{placeholder}
	bind:value
	{rows}
	{cols}
	{disabled}
	{required}
	class={classes()}
	{...restProps}
></textarea>