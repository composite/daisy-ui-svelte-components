<script lang="ts">
	interface Tab {
		id: string;
		label: string;
		content?: any;
		disabled?: boolean;
	}

	interface Props {
		tabs: Tab[];
		activeTab?: string;
		variant?: 'bordered' | 'lifted' | 'boxed';
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		class?: string;
		onChange?: (tabId: string) => void;
	}

	let {
		tabs,
		activeTab = $bindable(tabs[0]?.id),
		variant,
		size,
		class: className,
		onChange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'tabs';
		
		if (variant === 'bordered') result += ' tabs-bordered';
		if (variant === 'lifted') result += ' tabs-lifted';
		if (variant === 'boxed') result += ' tabs-boxed';
		if (size) result += ` tabs-${size}`;
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleTabChange(tabId: string, disabled?: boolean) {
		if (!disabled && tabId !== activeTab) {
			activeTab = tabId;
			onChange?.(tabId);
		}
	}

	let activeTabContent = $derived(() => {
		return tabs.find(tab => tab.id === activeTab)?.content;
	});
</script>

<div {...restProps}>
	<div role="tablist" class={classes()}>
		{#each tabs as tab}
			<button 
				role="tab" 
				class="tab{activeTab === tab.id ? ' tab-active' : ''}{tab.disabled ? ' tab-disabled' : ''}"
				disabled={tab.disabled}
				onclick={() => handleTabChange(tab.id, tab.disabled)}
			>
				{tab.label}
			</button>
		{/each}
	</div>
	
	{#if activeTabContent}
		<div class="tab-content">
			{@render activeTabContent()}
		</div>
	{/if}
</div>