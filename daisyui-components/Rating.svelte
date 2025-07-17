<script lang="ts">
	interface Props {
		value?: number;
		max?: number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		variant?: 'star' | 'heart' | 'thumb';
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		readonly?: boolean;
		half?: boolean;
		class?: string;
		onChange?: (value: number) => void;
	}

	let {
		value = $bindable(0),
		max = 5,
		size = 'md',
		variant = 'star',
		color,
		readonly = false,
		half = false,
		class: className,
		onChange,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'rating';
		
		if (size) result += ` rating-${size}`;
		if (half) result += ' rating-half';
		if (className) result += ` ${className}`;
		
		return result;
	});

	let radioClasses = $derived(() => {
		let result = `rating-${variant}`;
		
		if (color) result += ` rating-${color}`;
		
		return result;
	});

	function handleRatingChange(newValue: number) {
		if (!readonly) {
			value = newValue;
			onChange?.(newValue);
		}
	}

	let items = $derived(() => {
		const result = [];
		
		// Reset option
		result.push({ value: 0, hidden: true });
		
		for (let i = 1; i <= max; i++) {
			if (half) {
				result.push({ value: i - 0.5, half: true });
			}
			result.push({ value: i, half: false });
		}
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{#each items as item}
		<input 
			type="radio" 
			name="rating" 
			class="{radioClasses()}{item.half ? ' rating-half' : ''}{item.hidden ? ' rating-hidden' : ''}"
			checked={value === item.value}
			disabled={readonly}
			onchange={() => handleRatingChange(item.value)}
		/>
	{/each}
</div>