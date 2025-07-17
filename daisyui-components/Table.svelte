<script lang="ts">
	interface Column {
		key: string;
		label: string;
		sortable?: boolean;
		render?: (value: any, row: any) => any;
	}

	interface Props {
		columns: Column[];
		data: any[];
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
		zebra?: boolean;
		pinRows?: boolean;
		pinCols?: boolean;
		class?: string;
	}

	let {
		columns,
		data,
		size,
		zebra = false,
		pinRows = false,
		pinCols = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'table';
		
		if (size) result += ` table-${size}`;
		if (zebra) result += ' table-zebra';
		if (pinRows) result += ' table-pin-rows';
		if (pinCols) result += ' table-pin-cols';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class="overflow-x-auto">
	<table class={classes()} {...restProps}>
		<thead>
			<tr>
				{#each columns as column}
					<th>{column.label}</th>
				{/each}
			</tr>
		</thead>
		<tbody>
			{#each data as row, index}
				<tr>
					{#each columns as column}
						<td>
							{#if column.render}
								{@render column.render(row[column.key], row)}
							{:else}
								{row[column.key]}
							{/if}
						</td>
					{/each}
				</tr>
			{/each}
		</tbody>
	</table>
</div>