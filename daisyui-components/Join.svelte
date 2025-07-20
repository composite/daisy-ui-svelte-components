<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	const directions = {
		horizontal: 'join-horizontal',
		vertical: 'join-vertical'
	} as const;

	type Props = SvelteHTMLElements['div'] & {
		direction?: keyof typeof directions;
	} & RefElement<HTMLDivElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		direction = 'horizontal',
		class: className,
		children,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(cn('join', direction && directions[direction], className));
</script>

<div class={classes} bind:this={ref} {...restProps}>
	{@render children?.()}
</div>

<style lang="postcss">
	@reference 'tailwindcss';

	.join > :global(*) {
		@apply join-item;
	}
</style>
