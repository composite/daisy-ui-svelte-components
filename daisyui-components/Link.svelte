<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		nautral: 'link-neutral',
		primary: 'link-primary',
		secondary: 'link-secondary',
		accent: 'link-accent',
		info: 'link-info',
		success: 'link-success',
		warning: 'link-warning',
		error: 'link-error'
	} as const;
	type Props = SvelteHTMLElements['a'] & {
		color?: keyof typeof colors;
		hover?: boolean;
	} & RefElement<HTMLAnchorElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		color,
		hover = false,
		class: className,
		children,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(cn('link', color && colors[color], hover && 'link-hover', className));
</script>

<a class={classes} bind:this={ref} {...restProps}>
	{@render children?.()}
</a>
