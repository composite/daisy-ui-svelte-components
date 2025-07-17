<script lang="ts">
	interface ListItem {
		id: string;
		content: any[];
		wrapColumns?: number[];
		growColumn?: number;
	}

	interface Props {
		items: ListItem[];
		class?: string;
	}

	let {
		items,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'list';
		
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<ul class={classes()} {...restProps}>
	{#each items as item (item.id)}
		<li class="list-row">
			{#each item.content as content, index}
				<div 
					class={item.wrapColumns?.includes(index) ? 'list-col-wrap' : 
						   item.growColumn === index ? 'list-col-grow' : ''}
				>
					{@render content()}
				</div>
			{/each}
		</li>
	{/each}
</ul>