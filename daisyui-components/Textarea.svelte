<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'textarea-neutral',
		primary: 'textarea-primary',
		secondary: 'textarea-secondary',
		accent: 'textarea-accent',
		info: 'textarea-info',
		success: 'textarea-success',
		warning: 'textarea-warning',
		error: 'textarea-error'
	} as const;
	const sizes = {
		xs: 'textarea-xs',
		sm: 'textarea-sm',
		md: 'textarea-md',
		lg: 'textarea-lg',
		xl: 'textarea-xl'
	} as const;
	type Props = SvelteHTMLElements['textarea'] & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
		ghost?: boolean;
	} & RefElement<HTMLTextAreaElement>;
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
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn(
			'textarea',
			ghost && 'textarea-ghost',
			color && colors[color],
			size && sizes[size],
			className
		)
	);
</script>

<textarea bind:value class={classes} bind:this={ref} {...restProps}></textarea>
