<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';

	type Props = SvelteHTMLElements['div'] & {
		value: number;
		size?: string;
		thickness?: string;
	};
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		value = 0,
		size,
		thickness,
		class: className,
		style,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(cn('radial-progress', className));

	let styles = $derived.by(() => {
		let styling = '';
		if (value && !isNaN(+value)) styling += `--value: ${value};`;
		if (size) styling += `--size: ${size};`;
		if (thickness) styling += `--thickness: ${thickness};`;
		return `${styling}${style}`;
	});
</script>

<div
	class={classes}
	style={styles}
	role="progressbar"
	aria-valuenow={value}
	aria-valuemin="0"
	aria-valuemax="100"
	{...restProps}
>
	{#if children}
		{@render children()}
	{:else}
		{value}%
	{/if}
</div>
