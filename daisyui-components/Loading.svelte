<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const variants = {
		spinner: 'loading-spinner',
		dots: 'loading-dots',
		ring: 'loading-ring',
		ball: 'loading-ball',
		bars: 'loading-bars',
		infinity: 'loading-infinity'
	} as const;
	const sizes = {
		xs: 'loading-xs',
		sm: 'loading-sm',
		md: 'loading-md',
		lg: 'loading-lg',
		xl: 'loading-xl'
	} as const;
	type Props = Omit<SvelteHTMLElements['span'], 'children'> & {
		variant?: keyof typeof variants;
		size?: keyof typeof sizes;
	} & RefElement<HTMLSpanElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		variant = 'spinner',
		size,
		class: className,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn('loading', variant && variants[variant], size && sizes[size], className)
	);
</script>

<span class={classes} bind:this={ref} {...restProps}></span>
