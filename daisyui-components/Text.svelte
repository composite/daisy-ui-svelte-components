<script lang="ts">
	interface Props {
		as?: 'p' | 'span' | 'div' | 'h1' | 'h2' | 'h3' | 'h4' | 'h5' | 'h6';
		size?: 'xs' | 'sm' | 'base' | 'lg' | 'xl' | '2xl' | '3xl' | '4xl' | '5xl' | '6xl';
		weight?: 'thin' | 'extralight' | 'light' | 'normal' | 'medium' | 'semibold' | 'bold' | 'extrabold' | 'black';
		align?: 'left' | 'center' | 'right' | 'justify';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		opacity?: number;
		truncate?: boolean;
		uppercase?: boolean;
		lowercase?: boolean;
		capitalize?: boolean;
		class?: string;
		children?: any;
	}

	let {
		as = 'p',
		size,
		weight,
		align,
		color,
		opacity,
		truncate = false,
		uppercase = false,
		lowercase = false,
		capitalize = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = '';
		
		if (size) result += ` text-${size}`;
		if (weight) result += ` font-${weight}`;
		if (align) result += ` text-${align}`;
		if (color) result += ` text-${color}`;
		if (opacity) result += ` opacity-${opacity}`;
		if (truncate) result += ' truncate';
		if (uppercase) result += ' uppercase';
		if (lowercase) result += ' lowercase';
		if (capitalize) result += ' capitalize';
		if (className) result += ` ${className}`;
		
		return result.trim();
	});
</script>

<svelte:element this={as} class={classes()} {...restProps}>
	{@render children?.()}
</svelte:element>