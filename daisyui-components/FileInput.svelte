<script lang="ts">
	interface Props {
		variant?: 'primary' | 'secondary' | 'accent' | 'neutral' | 'info' | 'success' | 'warning' | 'error';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		ghost?: boolean;
		disabled?: boolean;
		multiple?: boolean;
		accept?: string;
		class?: string;
		files?: FileList;
		onchange?: (files: FileList | null) => void;
	}

	let {
		variant,
		size,
		ghost = false,
		disabled = false,
		multiple = false,
		accept,
		class: className,
		files = $bindable(),
		onchange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'file-input';
		
		if (variant) result += ` file-input-${variant}`;
		if (size) result += ` file-input-${size}`;
		if (ghost) result += ' file-input-ghost';
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleChange(event: Event) {
		const input = event.target as HTMLInputElement;
		files = input.files;
		onchange?.(input.files);
	}
</script>

<input 
	type="file" 
	class={classes()} 
	{disabled}
	{multiple}
	{accept}
	onchange={handleChange}
	{...restProps} 
/>
