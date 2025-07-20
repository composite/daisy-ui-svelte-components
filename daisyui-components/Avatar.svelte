<script lang="ts">
	import type { SvelteHTMLElements } from 'svelte/elements';
	import type { ClassValue } from 'clsx';
	import { cn } from '$lib/utils/doms';
	import type { RefElement } from '$components/ui/index';

	type Props = SvelteHTMLElements['div'] & {
		parentClass?: ClassValue;
		status?: 'online' | 'offline';
		placeholder?: boolean;
	} & RefElement<HTMLDivElement>;

	let {
		status,
		placeholder,
		parentClass,
		children,
		ref = $bindable(null),
		...restProps
	}: Props = $props();
</script>

<div
	class={cn('avatar', parentClass)}
	class:avatar-placeholder={placeholder}
	class:avatar-offline={status === 'offline'}
	class:avatar-online={status === 'online'}
	bind:this={ref}
>
	<div {...restProps}>
		{@render children?.()}
	</div>
</div>
