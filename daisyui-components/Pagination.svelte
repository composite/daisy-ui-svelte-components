<script lang="ts">
	interface Props {
		currentPage: number;
		totalPages: number;
		showPages?: number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		class?: string;
		onPageChange?: (page: number) => void;
	}

	let {
		currentPage,
		totalPages,
		showPages = 5,
		size,
		class: className,
		onPageChange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'join';
		
		if (className) result += ` ${className}`;
		
		return result;
	});

	let buttonClasses = $derived(() => {
		let result = 'join-item btn';
		
		if (size) result += ` btn-${size}`;
		
		return result;
	});

	let pages = $derived(() => {
		const start = Math.max(1, currentPage - Math.floor(showPages / 2));
		const end = Math.min(totalPages, start + showPages - 1);
		const adjustedStart = Math.max(1, end - showPages + 1);
		
		return Array.from({ length: end - adjustedStart + 1 }, (_, i) => adjustedStart + i);
	});

	function goToPage(page: number) {
		if (page >= 1 && page <= totalPages && page !== currentPage) {
			onPageChange?.(page);
		}
	}
</script>

<div class={classes()} {...restProps}>
	<!-- Previous button -->
	<button 
		class={buttonClasses()}
		disabled={currentPage === 1}
		onclick={() => goToPage(currentPage - 1)}
	>
		«
	</button>

	<!-- Page numbers -->
	{#each pages as page}
		<button 
			class="{buttonClasses()}{page === currentPage ? ' btn-active' : ''}"
			onclick={() => goToPage(page)}
		>
			{page}
		</button>
	{/each}

	<!-- Next button -->
	<button 
		class={buttonClasses()}
		disabled={currentPage === totalPages}
		onclick={() => goToPage(currentPage + 1)}
	>
		»
	</button>
</div>
