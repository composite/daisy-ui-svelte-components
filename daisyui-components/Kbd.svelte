<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const sizes = {
		xs: 'kbd-xs',
		sm: 'kbd-sm',
		md: 'kbd-md',
		lg: 'kbd-lg',
		xl: 'kbd-xl'
	} as const;
	type Props = SvelteHTMLElements['kbd'] & {
		size?: keyof typeof sizes;
	} & RefElement;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let { size, class: className, children, ref = $bindable(null), ...restProps }: Props = $props();

	let classes = $derived(cn('kbd', size && sizes[size], className));
</script>

<kbd class={classes} bind:this={ref} {...restProps}>
	{@render children?.()}
</kbd>
