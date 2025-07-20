<script lang="ts">
	interface Props {
		value?: number;
		max?: number;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		variant?: 'star' | 'heart' | 'thumb';
		color?:
			| 'neutral'
			| 'primary'
			| 'secondary'
			| 'accent'
			| 'info'
			| 'success'
			| 'warning'
			| 'error';
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

		// Size classes
		if (size === 'xs') result += ' rating-xs';
		if (size === 'sm') result += ' rating-sm';
		if (size === 'md') result += ' rating-md';
		if (size === 'lg') result += ' rating-lg';
		if (size === 'xl') result += ' rating-xl';

		if (half) result += ' rating-half';
		if (className) result += ` ${className}`;

		return result;
	});

	let radioClasses = $derived(() => {
		let result = '';

		// Variant classes
		if (variant === 'star') result += 'rating-star';
		if (variant === 'heart') result += 'rating-heart';
		if (variant === 'thumb') result += 'rating-thumb';

		// Color classes
		if (color === 'neutral') result += ' rating-neutral';
		if (color === 'primary') result += ' rating-primary';
		if (color === 'secondary') result += ' rating-secondary';
		if (color === 'accent') result += ' rating-accent';
		if (color === 'info') result += ' rating-info';
		if (color === 'success') result += ' rating-success';
		if (color === 'warning') result += ' rating-warning';
		if (color === 'error') result += ' rating-error';

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
	{#each items() as item (item.value)}
		<input
			type="radio"
			name="rating"
			class={radioClasses()}
			class:rating-half={item.half}
			class:rating-hidden={item.hidden}
			checked={value === item.value}
			disabled={readonly}
			onchange={() => handleRatingChange(item.value)}
		/>
	{/each}
</div>
