<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { RefElement } from '$components/ui';

	const colors = {
		neutral: 'progress-neutral',
		primary: 'progress-primary',
		secondary: 'progress-secondary',
		accent: 'progress-accent',
		info: 'progress-info',
		success: 'progress-success',
		warning: 'progress-warning',
		error: 'progress-error'
	} as const;
	type Props = SvelteHTMLElements['progress'] & {
		color?: keyof typeof colors;
	} & RefElement<HTMLProgressElement>;
</script>

<script lang="ts">
	import { cn } from '$lib/utils/doms';

	let { max = 100, color, class: className, children, ...restProps }: Props = $props();

	let classes = $derived(cn('progress', color && colors[color], className));
</script>

<progress class={classes} {max} {...restProps}>{children?.()}</progress>
