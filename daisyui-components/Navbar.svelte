<script lang="ts">
	interface Props {
		sticky?: boolean;
		class?: string;
		start?: any;
		center?: any;
		end?: any;
	}

	let { sticky = false, class: className, start, center, end, ...restProps }: Props = $props();

	let classes = $derived(() => {
		let result = 'navbar';

		if (sticky) result += ' sticky top-0 z-30';
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	<div class="navbar-start">
		{#if start}
			{@render start()}
		{/if}
	</div>
	<div class="navbar-center">
		{#if center}
			{@render center()}
		{/if}
	</div>
	<div class="navbar-end">
		{#if end}
			{@render end()}
		{/if}
	</div>
</div>
