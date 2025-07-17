<script lang="ts">
	interface Props {
		position?: 'top' | 'bottom' | 'left' | 'right';
		align?: 'start' | 'center' | 'end';
		hover?: boolean;
		open?: boolean;
		class?: string;
		trigger?: any;
		children?: any;
	}

	let {
		position,
		align,
		hover = false,
		open = $bindable(false),
		class: className,
		trigger,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'dropdown';
		
		if (position) result += ` dropdown-${position}`;
		if (align) result += ` dropdown-${align}`;
		if (hover) result += ' dropdown-hover';
		if (open) result += ' dropdown-open';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	<div tabindex="0" role="button" class="btn">
		{#if trigger}
			{@render trigger()}
		{/if}
	</div>
	<div tabindex="0" class="dropdown-content menu bg-base-100 rounded-box z-[1] w-52 p-2 shadow">
		{@render children?.()}
	</div>
</div>
