<script lang="ts">
	interface Props {
		variant?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
		alignment: 'start' | 'end';
		avatar?: any;
		header?: string;
		footer?: string;
		time?: string;
		class?: string;
		children?: any;
	}

	let {
		variant,
		alignment,
		avatar,
		header,
		footer,
		time,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'chat';
		
		if (alignment) result += ` chat-${alignment}`;
		if (className) result += ` ${className}`;
		
		return result;
	});

	let bubbleClasses = $derived(() => {
		let result = 'chat-bubble';
		
		if (variant) result += ` chat-bubble-${variant}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{#if avatar}
		<div class="chat-image avatar">
			{@render avatar()}
		</div>
	{/if}
	{#if header}
		<div class="chat-header">
			{header}
			{#if time}
				<time class="text-xs opacity-50">{time}</time>
			{/if}
		</div>
	{/if}
	<div class={bubbleClasses()}>
		{@render children?.()}
	</div>
	{#if footer}
		<div class="chat-footer opacity-50">
			{footer}
		</div>
	{/if}
</div>
