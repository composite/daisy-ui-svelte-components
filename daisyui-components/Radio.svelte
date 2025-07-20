<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'radio-neutral',
		primary: 'radio-primary',
		secondary: 'radio-secondary',
		accent: 'radio-accent',
		info: 'radio-info',
		success: 'radio-success',
		warning: 'radio-warning',
		error: 'radio-error'
	} as const;
	const sizes = {
		xs: 'radio-xs',
		sm: 'radio-sm',
		md: 'radio-md',
		lg: 'radio-lg',
		xl: 'radio-xl'
	} as const;
	type Props = Omit<SvelteHTMLElements['input'], 'type'> & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
	} & RefElement<HTMLInputElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		group = $bindable(),
		size,
		color,
		class: className,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(cn('radio', color && colors[color], size && sizes[size], className));
</script>

<input type="radio" bind:group class={classes} bind:this={ref} {...restProps} />
