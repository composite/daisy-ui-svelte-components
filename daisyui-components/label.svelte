<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui/index';

	type Props = SvelteHTMLElements['label'] & {
		floating?: boolean;
	} & RefElement<HTMLLabelElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let {
		floating,
		class: className,
		children,
		ref = $bindable(null),
		...restProps
	}: Props = $props();

	let classes = $derived(cn(floating && 'floating-label', className));
</script>

<label class={classes} bind:this={ref} {...restProps}>
	{@render children?.()}
</label>

<style lang="postcss">
	label:not(.floating-label) > :global(span) {
		@apply label;
	}
	label:not(.floating-label):has(:global(> input)) {
		@apply input;
	}
	label:not(.floating-label):has(:global(> select)) {
		@apply select;
	}
</style>
