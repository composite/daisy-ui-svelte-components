<script lang="ts">
	interface Props {
		align?: 'top' | 'bottom' | 'start' | 'end';
		class?: string;
		children?: any;
	}

	let { align, class: className, children, ...restProps }: Props = $props();

	let classes = $derived(() => {
		let result = 'stack';

		if (align === 'top') result += ' stack-top';
		if (align === 'bottom') result += ' stack-bottom';
		if (align === 'start') result += ' stack-start';
		if (align === 'end') result += ' stack-end';
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>
