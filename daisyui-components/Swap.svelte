<script lang="ts">
	interface Props {
		active?: boolean;
		rotate?: boolean;
		flip?: boolean;
		class?: string;
		onIcon?: any;
		offIcon?: any;
		onChange?: (active: boolean) => void;
	}

	let {
		active = $bindable(false),
		rotate = false,
		flip = false,
		class: className,
		onIcon,
		offIcon,
		onChange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'swap';
		
		if (rotate) result += ' swap-rotate';
		if (flip) result += ' swap-flip';
		if (active) result += ' swap-active';
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleChange() {
		active = !active;
		onChange?.(active);
	}
</script>

<label class={classes()} {...restProps}>
	<input type="checkbox" bind:checked={active} onchange={handleChange} />
	
	{#if onIcon}
		<div class="swap-on">
			{@render onIcon()}
		</div>
	{/if}
	
	{#if offIcon}
		<div class="swap-off">
			{@render offIcon()}
		</div>
	{/if}
</label>