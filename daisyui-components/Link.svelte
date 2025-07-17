<script lang="ts">
	interface Props {
		variant?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		hover?: boolean;
		href?: string;
		target?: '_blank' | '_self' | '_parent' | '_top';
		class?: string;
		children?: any;
		onclick?: () => void;
	}

	let {
		variant,
		hover = false,
		href,
		target,
		class: className,
		children,
		onclick,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'link';
		
		if (variant) result += ` link-${variant}`;
		if (hover) result += ' link-hover';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<a {href} {target} class={classes()} {onclick} {...restProps}>
	{@render children?.()}
</a>
