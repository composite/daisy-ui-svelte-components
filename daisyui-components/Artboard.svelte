<script lang="ts">
	interface Props {
		size?: '1' | '2' | '3' | '4' | '5' | '6';
		horizontal?: boolean;
		demo?: boolean;
		class?: string;
		children?: any;
	}

	let {
		size = '1',
		horizontal = false,
		demo = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'artboard';
		
		if (size) result += ` artboard-${size}`;
		if (horizontal) result += ' artboard-horizontal';
		if (demo) result += ' artboard-demo';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{@render children?.()}
</div>