<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'input-neutral',
		primary: 'input-primary',
		secondary: 'input-secondary',
		accent: 'input-accent',
		info: 'input-info',
		success: 'input-success',
		warning: 'input-warning',
		error: 'input-error'
	} as const;
	const sizes = {
		xs: 'input-xs',
		sm: 'input-sm',
		md: 'input-md',
		lg: 'input-lg',
		xl: 'input-xl'
	} as const;
	type Props = SvelteHTMLElements['input'] & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
		ghost?: boolean;
	} & RefElement<HTMLInputElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		type = 'text',
		value = $bindable(),
		size,
		color,
		ghost = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn('input', ghost && 'input-ghost', color && colors[color], size && sizes[size], className)
	);
</script>

<input {type} bind:value class={classes} {...restProps} />
