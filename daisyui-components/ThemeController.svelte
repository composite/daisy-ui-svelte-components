<script lang="ts">
	interface Props {
		type?: 'checkbox' | 'radio' | 'toggle' | 'swap' | 'button';
		theme: string;
		checked?: boolean;
		name?: string;
		label?: string;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		class?: string;
		onIcon?: any;
		offIcon?: any;
		children?: any;
		onchange?: (theme: string, checked: boolean) => void;
	}

	let {
		type = 'checkbox',
		theme,
		checked = $bindable(false),
		name,
		label,
		size,
		class: className,
		onIcon,
		offIcon,
		children,
		onchange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'theme-controller';
		
		if (type === 'toggle') result += ' toggle';
		if (type === 'checkbox') result += ' checkbox';
		if (type === 'radio') result += ' radio';
		if (type === 'button') result += ' btn';
		if (type === 'swap') result += ' swap swap-rotate';
		
		if (size) {
			if (type === 'toggle') result += ` toggle-${size}`;
			if (type === 'checkbox') result += ` checkbox-${size}`;
			if (type === 'radio') result += ` radio-${size}`;
			if (type === 'button') result += ` btn-${size}`;
		}
		
		if (className) result += ` ${className}`;
		
		return result;
	});

	function handleChange() {
		onchange?.(theme, checked);
	}
</script>

{#if type === 'swap'}
	<label class="swap swap-rotate">
		<input 
			type="checkbox" 
			class={classes()}
			value={theme}
			bind:checked
			onchange={handleChange}
			{...restProps}
		/>
		
		{#if offIcon}
			<div class="swap-off">
				{@render offIcon()}
			</div>
		{/if}
		
		{#if onIcon}
			<div class="swap-on">
				{@render onIcon()}
			</div>
		{/if}
	</label>
{:else if type === 'button'}
	<input 
		type="radio"
		{name}
		class={classes()}
		value={theme}
		checked={checked}
		aria-label={label || theme}
		onchange={handleChange}
		{...restProps}
	/>
{:else if type === 'radio'}
	<label class="flex gap-2 cursor-pointer items-center">
		<input 
			type="radio"
			{name}
			class={classes()}
			value={theme}
      checked={checked}
			onchange={handleChange}
			{...restProps}
		/>
		{label || theme}
	</label>
{:else}
	{#if label}
		<label class="flex cursor-pointer gap-2">
			{#if children}
				{@render children()}
			{:else}
				<span class="label-text">{label}</span>
			{/if}
			<input 
				type={type}
				class={classes()}
				value={theme}
        checked={checked}
				onchange={handleChange}
				{...restProps}
			/>
		</label>
	{:else}
		<input 
			type={type}
			class={classes()}
			value={theme}
      checked={checked}
			onchange={handleChange}
			{...restProps}
		/>
	{/if}
{/if}