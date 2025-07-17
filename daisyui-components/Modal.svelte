<script lang="ts">
	interface Props {
		open?: boolean;
		position?: 'top' | 'middle' | 'bottom' | 'start' | 'end';
		responsive?: boolean;
		class?: string;
		children?: any;
		actions?: any;
		onClose?: () => void;
	}

	let {
		open = $bindable(false),
		position,
		responsive = false,
		class: className,
		children,
		actions,
		onClose,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'modal';
		
		if (position) result += ` modal-${position}`;
		if (responsive) result += ' modal-responsive';
		if (open) result += ' modal-open';
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleClose() {
		open = false;
		onClose?.();
	}

	function handleBackdropClick(event: Event) {
		if (event.target === event.currentTarget) {
			handleClose();
		}
	}
</script>

<dialog class={classes()} {...restProps} onclick={handleBackdropClick}>
	<div class="modal-box">
		<form method="dialog">
			<button class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2" onclick={handleClose}>✕</button>
		</form>
		{@render children?.()}
		{#if actions}
			<div class="modal-action">
				{@render actions()}
			</div>
		{/if}
	</div>
</dialog>
