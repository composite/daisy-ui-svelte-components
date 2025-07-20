<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'select-neutral',
		primary: 'select-primary',
		secondary: 'select-secondary',
		accent: 'select-accent',
		info: 'select-info',
		success: 'select-success',
		warning: 'select-warning',
		error: 'select-error'
	} as const;
	const sizes = {
		xs: 'select-xs',
		sm: 'select-sm',
		md: 'select-md',
		lg: 'select-lg',
		xl: 'select-xl'
	} as const;
	type Props = SvelteHTMLElements['select'] & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
		ghost?: boolean;
	} & RefElement<HTMLSelectElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		value = $bindable(),
		size,
		color,
		ghost = false,
		class: className,
		ref = $bindable(null),
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn('select', ghost && 'select-ghost', color && colors[color], size && sizes[size], className)
	);
</script>

<select bind:value class={classes} bind:this={ref} {...restProps}>
	{children?.()}
</select>
