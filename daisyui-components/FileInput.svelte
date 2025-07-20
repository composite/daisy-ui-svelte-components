<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'file-input-neutral',
		primary: 'file-input-primary',
		secondary: 'file-input-secondary',
		accent: 'file-input-accent',
		info: 'file-input-info',
		success: 'file-input-success',
		warning: 'file-input-warning',
		error: 'file-input-error'
	} as const;
	const sizes = {
		xs: 'file-input-xs',
		sm: 'file-input-sm',
		md: 'file-input-md',
		lg: 'file-input-lg',
		xl: 'file-input-xl'
	} as const;
	type Props = Omit<SvelteHTMLElements['input'], 'type'> & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
		ghost?: boolean;
	} & RefElement<HTMLInputElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		files = $bindable(),
		size,
		color,
		ghost = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn('input', ghost && 'file-input-ghost', color && colors[color], size && sizes[size], className)
	);
</script>

<input type="file" bind:files class={classes} {...restProps} />
