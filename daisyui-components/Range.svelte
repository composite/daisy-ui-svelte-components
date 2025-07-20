<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'range-neutral',
		primary: 'range-primary',
		secondary: 'range-secondary',
		accent: 'range-accent',
		info: 'range-info',
		success: 'range-success',
		warning: 'range-warning',
		error: 'range-error'
	} as const;
	const sizes = {
		xs: 'range-xs',
		sm: 'range-sm',
		md: 'range-md',
		lg: 'range-lg',
		xl: 'range-xl'
	} as const;
	type Props = Omit<SvelteHTMLElements['input'], 'type'> & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
	} & RefElement<HTMLInputElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let { size, color, class: className, ref = $bindable(null), ...restProps }: Props = $props();

	let classes = $derived(cn('range', color && colors[color], size && sizes[size], className));
</script>

<input type="range" class={classes} bind:this={ref} {...restProps} />
