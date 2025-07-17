<script lang="ts">
	interface ToastItem {
		id: string;
		message: string;
		type?: 'info' | 'success' | 'warning' | 'error';
		duration?: number;
		dismissible?: boolean;
	}

	interface Props {
		toasts: ToastItem[];
		position?: 'top-start' | 'top-center' | 'top-end' | 'middle-start' | 'middle-center' | 'middle-end' | 'bottom-start' | 'bottom-center' | 'bottom-end';
		class?: string;
		onDismiss?: (id: string) => void;
	}

	let {
		toasts,
		position = 'top-end',
		class: className,
		onDismiss,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'toast';
		
		// Position classes
		if (position === 'top-start') result += ' toast-top-start';
		if (position === 'top-center') result += ' toast-top-center';
		if (position === 'top-end') result += ' toast-top-end';
		if (position === 'middle-start') result += ' toast-middle-start';
		if (position === 'middle-center') result += ' toast-middle-center';
		if (position === 'middle-end') result += ' toast-middle-end';
		if (position === 'bottom-start') result += ' toast-bottom-start';
		if (position === 'bottom-center') result += ' toast-bottom-center';
		if (position === 'bottom-end') result += ' toast-bottom-end';
		
		if (className) result += ` ${className}`;
		
		return result;
	});

	function dismissToast(id: string) {
		onDismiss?.(id);
	}

	// Auto-dismiss toasts with duration
	$effect(() => {
		toasts.forEach(toast => {
			if (toast.duration && toast.duration > 0) {
				setTimeout(() => {
					dismissToast(toast.id);
				}, toast.duration);
			}
		});
	});
</script>

<div class={classes()} {...restProps}>
	{#each toasts as toast (toast.id)}
		<div class="alert{toast.type === 'info' ? ' alert-info' : toast.type === 'success' ? ' alert-success' : toast.type === 'warning' ? ' alert-warning' : toast.type === 'error' ? ' alert-error' : ''}" role="alert">
			<span>{toast.message}</span>
			{#if toast.dismissible}
				<button 
					onclick={() => dismissToast(toast.id)}
					class="btn btn-sm btn-circle btn-ghost"
				>
					<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
					</svg>
				</button>
			{/if}
		</div>
	{/each}
</div>