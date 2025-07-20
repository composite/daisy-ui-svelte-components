<script lang="ts">
	interface Props {
		text: string;
		position?: 'top' | 'bottom' | 'left' | 'right';
		color?:
			| 'neutral'
			| 'primary'
			| 'secondary'
			| 'accent'
			| 'info'
			| 'success'
			| 'warning'
			| 'error';
		open?: boolean;
		class?: string;
		children?: any;
	}

	let {
		text,
		position = 'top',
		color,
		open = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'tooltip';

		if (position) result += ` tooltip-${position}`;
		if (color) result += ` tooltip-${color}`;
		if (open) result += ' tooltip-open';
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} data-tip={text} {...restProps}>
	{@render children?.()}
</div>
