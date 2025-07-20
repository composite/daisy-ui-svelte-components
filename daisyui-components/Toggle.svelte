<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		primary: 'toggle-primary',
		secondary: 'toggle-secondary',
		accent: 'toggle-accent',
		neutral: 'toggle-neutral',
		info: 'toggle-info',
		success: 'toggle-success',
		warning: 'toggle-warning',
		error: 'toggle-error'
	} as const;
	const sizes = {
		xs: 'toggle-xs',
		sm: 'toggle-sm',
		md: 'toggle-md',
		lg: 'toggle-lg',
		xl: 'toggle-xl'
	} as const;
	type Props = Omit<SvelteHTMLElements['input'], 'type'> & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
	} & RefElement<HTMLInputElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		color,
		size,
		checked = $bindable(),
		group = $bindable(),
		indeterminate = $bindable(),
		class: className,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(cn('toggle', color && colors[color], size && sizes[size], className));
</script>

<input
	type="checkbox"
	bind:checked
	bind:group
	bind:indeterminate
	class={classes}
	bind:this={ref}
	{...restProps}
/>
