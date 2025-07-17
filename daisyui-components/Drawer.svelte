<script lang="ts">
	interface Props {
		side?: 'end';
		open?: boolean;
		id?: string;
		class?: string;
		children?: any;
		sideContent?: any;
	}

	let {
		side,
		open = $bindable(false),
		id = 'my-drawer',
		class: className,
		children,
		sideContent,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'drawer';
		
		if (side) result += ` drawer-${side}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	<input {id} type="checkbox" bind:checked={open} class="drawer-toggle" />
	<div class="drawer-content">
		{@render children?.()}
	</div>
	<div class="drawer-side">
		<label for={id} aria-label="close sidebar" class="drawer-overlay"></label>
		{#if sideContent}
			{@render sideContent()}
		{/if}
	</div>
</div>
