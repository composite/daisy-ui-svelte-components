<script lang="ts">
	interface Props {
		value: number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		font?: 'mono';
		class?: string;
	}

	let {
		value,
		size,
		font,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'countdown';
		
		if (size) result += ` text-${size}`;
		if (font) result += ` font-${font}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<span class={classes()} style="--value:{value};" {...restProps}></span>
