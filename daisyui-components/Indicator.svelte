<script lang="ts">
	interface Props {
		position?:
			| 'top-start'
			| 'top-center'
			| 'top-end'
			| 'middle-start'
			| 'middle-center'
			| 'middle-end'
			| 'bottom-start'
			| 'bottom-center'
			| 'bottom-end';
		class?: string;
		indicator?: any;
		children?: any;
	}

	let { position, class: className, indicator, children, ...restProps }: Props = $props();

	let classes = $derived(() => {
		let result = 'indicator';

		if (className) result += ` ${className}`;

		return result;
	});

	let indicatorClasses = $derived(() => {
		let result = 'indicator-item';

		if (position) {
			const [vertical, horizontal] = position.split('-');
			if (vertical === 'top') result += ' indicator-top';
			if (vertical === 'bottom') result += ' indicator-bottom';
			if (vertical === 'middle') result += ' indicator-middle';

			if (horizontal === 'start') result += ' indicator-start';
			if (horizontal === 'end') result += ' indicator-end';
			if (horizontal === 'center') result += ' indicator-center';
		}

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{#if indicator}
		<span class={indicatorClasses()}>
			{@render indicator()}
		</span>
	{/if}
	{@render children?.()}
</div>
