<script lang="ts">
	interface Props {
		minHeight?: 'screen' | 'full' | string;
		class?: string;
		overlay?: any;
		children?: any;
	}

	let { minHeight = 'screen', class: className, overlay, children, ...restProps }: Props = $props();

	let classes = $derived(() => {
		let result = 'hero';

		if (minHeight === 'screen') result += ' min-h-screen';
		else if (minHeight === 'full') result += ' min-h-full';
		else if (minHeight) result += ` ${minHeight}`;
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{#if overlay}
		<div class="hero-overlay">
			{@render overlay()}
		</div>
	{/if}
	<div class="hero-content">
		{@render children?.()}
	</div>
</div>
