<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const shapes = {
		squircle: 'mask-squircle',
		heart: 'mask-heart',
		hexagon: 'mask-hexagon',
		'hexagon-2': 'mask-hexagon-2',
		decagon: 'mask-decagon',
		pentagon: 'mask-pentagon',
		diamond: 'mask-diamond',
		square: 'mask-square',
		circle: 'mask-circle',
		star: 'mask-star',
		'star-2': 'mask-star-2',
		triangle: 'mask-triangle',
		'triangle-2': 'mask-triangle-2',
		'triangle-3': 'mask-triangle-3',
		'triangle-4': 'mask-triangle-4',
		'half-1': 'mask-half-1',
		'half-2': 'mask-half-2'
	} as const;
	type Props<
		T extends keyof SvelteHTMLElements = 'img',
		E extends HTMLElement = HTMLImageElement
	> = SvelteHTMLElements[T] & {
		as?: T;
		shape?: keyof typeof shapes;
		class?: string;
	} & RefElement<E>;
</script>

<script
	lang="ts"
	generics="T extends keyof SvelteHTMLElements = 'img', E extends HTMLElement = HTMLImageElement"
>
	import { cn } from '$lib/utils/doms';

	let {
		as,
		shape,
		class: className,
		children,
		ref = $bindable(null),
		...restProps
	}: Props<T, E> = $props();

	let classes = $derived(cn('mask', shape && shapes[shape], className));
</script>

<svelte:element this={as} class={classes} bind:this={ref} {...restProps}>
	{@render children?.()}
</svelte:element>
