<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const colors = {
		neutral: 'badge-neutral',
		primary: 'badge-primary',
		secondary: 'badge-secondary',
		accent: 'badge-accent',
		info: 'badge-info',
		success: 'badge-success',
		warning: 'badge-warning',
		error: 'badge-error',
		ghost: 'badge-ghost'
	} as const;
	const sizes = {
		xs: 'badge-xs',
		sm: 'badge-sm',
		md: 'badge-md',
		lg: 'badge-lg',
		xl: 'badge-xl'
	} as const;
	const variants = {
		outline: 'badge-outline',
		dash: 'badge-dash',
		soft: 'badge-soft'
	};

	type Props = SvelteHTMLElements['span'] & {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
		variant?: keyof typeof variants;
	} & RefElement<HTMLSpanElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		variant,
		size,
		color,
		class: className,
		children,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn('badge', variant && variants[variant], size && sizes[size] && color && colors[color])
	);
</script>

<span class={[classes, className]} bind:this={ref} {...restProps}>
	{@render children?.()}
</span>
