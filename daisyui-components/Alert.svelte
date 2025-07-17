<script lang="ts">
	interface Props {
		variant?: 'info' | 'success' | 'warning' | 'error';
		style?: 'outline' | 'dash' | 'soft';
		direction?: 'vertical' | 'horizontal';
		dismissible?: boolean;
		icon?: any;
		class?: string;
		children?: any;
		onDismiss?: () => void;
	}

	let {
		variant,
		style,
		direction,
		dismissible = false,
		icon,
		class: className,
		children,
		onDismiss,
		...restProps
	}: Props = $props();

	let visible = $state(true);

	let classes = $derived(() => {
		let result = 'alert';
		
		if (variant) result += ` alert-${variant}`;
		if (style) result += ` alert-${style}`;
		if (direction) result += ` alert-${direction}`;
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleDismiss() {
		visible = false;
		onDismiss?.();
	}
</script>

{#if visible}
	<div role="alert" class={classes()} {...restProps}>
		{#if icon}
			{@render icon()}
		{/if}
		{@render children?.()}
		{#if dismissible}
			<button onclick={handleDismiss} class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2">
				<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
				</svg>
			</button>
		{/if}
	</div>
{/if}
