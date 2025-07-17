<script lang="ts">
	interface Props {
		class?: string;
		item1?: any;
		item2?: any;
	}

	let {
		class: className,
		item1,
		item2,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'diff';
		
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<figure class={classes()} {...restProps}>
	<div class="diff-item-1">
		{#if item1}
			{@render item1()}
		{/if}
	</div>
	<div class="diff-item-2">
		{#if item2}
			{@render item2()}
		{/if}
	</div>
	<div class="diff-resizer"></div>
</figure>
