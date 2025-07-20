<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		primary: 'checkbox-primary',
		secondary: 'checkbox-secondary',
		accent: 'checkbox-accent',
		neutral: 'checkbox-neutral',
		info: 'checkbox-info',
		success: 'checkbox-success',
		warning: 'checkbox-warning',
		error: 'checkbox-error'
	} as const;
	const sizes = {
		xs: 'checkbox-xs',
		sm: 'checkbox-sm',
		md: 'checkbox-md',
		lg: 'checkbox-lg',
		xl: 'checkbox-xl'
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

	let classes = $derived(cn('checkbox', color && colors[color], size && sizes[size], className));
</script>

<input
	type="checkbox"
	class={classes}
	bind:checked
	bind:group
	bind:indeterminate
	bind:this={ref}
	{...restProps}
/>
