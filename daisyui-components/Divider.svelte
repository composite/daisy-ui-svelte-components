<script lang="ts">
	interface Props {
		orientation?: 'horizontal' | 'vertical';
		position?: 'start' | 'end';
		color?:
			| 'neutral'
			| 'primary'
			| 'secondary'
			| 'accent'
			| 'info'
			| 'success'
			| 'warning'
			| 'error';
		text?: string;
		class?: string;
		children?: any;
	}

	let {
		orientation = 'horizontal',
		position,
		color,
		text,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'divider';

		if (orientation === 'vertical') result += ' divider-vertical';
		if (orientation === 'horizontal') result += ' divider-horizontal';
		if (position === 'start') result += ' divider-start';
		if (position === 'end') result += ' divider-end';
		if (color) result += ` divider-${color}`;
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{#if text}
		{text}
	{:else if children}
		{@render children()}
	{/if}
</div>
