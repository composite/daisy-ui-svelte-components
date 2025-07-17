<script lang="ts">
	interface Option {
		value: string | number;
		label: string;
		disabled?: boolean;
	}

	interface Props {
		options: Option[];
		value?: string | number;
		placeholder?: string;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		ghost?: boolean;
		disabled?: boolean;
		required?: boolean;
		multiple?: boolean;
		class?: string;
	}

	let {
		options,
		value = $bindable(),
		placeholder,
		size,
		color,
		ghost = false,
		disabled = false,
		required = false,
		multiple = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'select';
		
		if (ghost) result += ' select-ghost';
		if (size) result += ` select-${size}`;
		if (color) result += ` select-${color}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

{#if multiple}
  <select
    bind:value
    {disabled}
    {required}
    multiple
    class={classes()}
    {...restProps}
  >
    {#if placeholder && !multiple}
      <option value="" disabled selected={!value}>{placeholder}</option>
    {/if}
    {#each options as option (option.value)}
      <option value={option.value} disabled={option.disabled}>
        {option.label}
      </option>
    {/each}
  </select>
{:else}
  <select
    bind:value
    {disabled}
    {required}
    class={classes()}
    {...restProps}
  >
    {#if placeholder && !multiple}
      <option value="" disabled selected={!value}>{placeholder}</option>
    {/if}
    {#each options as option (option.value)}
      <option value={option.value} disabled={option.disabled}>
        {option.label}
      </option>
    {/each}
  </select>
{/if}
