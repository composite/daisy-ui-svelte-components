<script lang="ts">
	interface NavItem {
		id: string;
		label: string;
		icon?: any;
		active?: boolean;
		disabled?: boolean;
		href?: string;
	}

	interface Props {
		items: NavItem[];
		activeItem?: string;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		class?: string;
		onChange?: (itemId: string) => void;
	}

	let {
		items,
		activeItem = $bindable(),
		size,
		class: className,
		onChange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'btm-nav';
		
		// Size classes
		if (size === 'xs') result += ' btm-nav-xs';
		if (size === 'sm') result += ' btm-nav-sm';
		if (size === 'md') result += ' btm-nav-md';
		if (size === 'lg') result += ' btm-nav-lg';
		if (size === 'xl') result += ' btm-nav-xl';
		
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleItemClick(item: NavItem) {
		if (!item.disabled) {
			activeItem = item.id;
			onChange?.(item.id);
		}
	}
</script>

<div class={classes()} {...restProps}>
	{#each items as item}
		{#if item.href}
			<a 
				href={item.href}
				class:active={activeItem === item.id}
				class:disabled={item.disabled}
			>
				{#if item.icon}
					{@render item.icon()}
				{/if}
				<span class="btm-nav-label">{item.label}</span>
			</a>
		{:else}
			<button 
				class:active={activeItem === item.id}
				class:disabled={item.disabled}
				disabled={item.disabled}
				onclick={() => handleItemClick(item)}
			>
				{#if item.icon}
					{@render item.icon()}
				{/if}
				<span class="btm-nav-label">{item.label}</span>
			</button>
		{/if}
	{/each}
</div>