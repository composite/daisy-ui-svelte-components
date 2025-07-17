<script lang="ts">
	interface TimelineItem {
		id: string;
		startContent?: any;
		middleContent?: any;
		endContent?: any;
		snapIcon?: boolean;
		box?: boolean;
	}

	interface Props {
		items: TimelineItem[];
		direction?: 'horizontal' | 'vertical';
		compact?: boolean;
		class?: string;
	}

	let {
		items,
		direction = 'horizontal',
		compact = false,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'timeline';
		
		if (direction === 'vertical') result += ' timeline-vertical';
		if (direction === 'horizontal') result += ' timeline-horizontal';
		if (compact) result += ' timeline-compact';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<ul class={classes()} {...restProps}>
	{#each items as item (item.id)}
		<li>
			{#if item.startContent}
				<div class:timeline-box={item.box} class="timeline-start">
					{@render item.startContent()}
				</div>
			{/if}
			{#if item.middleContent}
				<div class:timeline-snap-icon={item.snapIcon} class="timeline-middle">
					{@render item.middleContent()}
				</div>
			{/if}
			{#if item.endContent}
				<div class:timeline-box={item.box} class="timeline-end">
					{@render item.endContent()}
				</div>
			{/if}
		</li>
	{/each}
</ul>