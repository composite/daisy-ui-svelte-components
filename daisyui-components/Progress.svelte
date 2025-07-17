<script lang="ts">
	interface Props {
		value?: number;
		max?: number;
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		indeterminate?: boolean;
		class?: string;
	}

	let {
		value,
		max = 100,
		color,
		size,
		indeterminate = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'progress';
		
		if (color) result += ` progress-${color}`;
		if (size) result += ` progress-${size}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<progress
	class={classes()}
	value={indeterminate ? undefined : value}
	{max}
	{...restProps}
></progress>