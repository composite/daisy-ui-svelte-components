<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';

	const sizes = {
		xs: 'card-xs',
		sm: 'card-sm',
		md: 'card-md',
		lg: 'card-lg',
		xl: 'card-xl'
	} as const;
	const variants = {
		border: 'card-border',
		dash: 'card-dash'
	} as const;
	type Props = SvelteHTMLElements['div'] & {
		size?: keyof typeof sizes;
		variant?: keyof typeof variants;
		side?: boolean;
		imageFull?: boolean;
	};
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		size,
		variant,
		side = false,
		imageFull = false,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(
		cn(
			'card',
			size && sizes[size],
			variant && variants[variant],
			side && 'card-side',
			imageFull && 'image-full',
			className
		)
	);
</script>

<div class={classes} {...restProps}>
	{@render children?.()}
</div>
