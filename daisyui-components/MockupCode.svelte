<script lang="ts">
	interface CodeLine {
		content: string;
		prefix?: string;
		highlight?: boolean;
		textColor?: string;
		backgroundColor?: string;
	}

	interface Props {
		lines: CodeLine[];
		backgroundColor?: string;
		textColor?: string;
		class?: string;
	}

	let {
		lines,
		backgroundColor,
		textColor,
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'mockup-code';
		
		if (backgroundColor) result += ` ${backgroundColor}`;
		if (textColor) result += ` ${textColor}`;
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	{#each lines as line}
		<pre 
			data-prefix={line.prefix || ''}
			class="{line.highlight ? 'bg-warning text-warning-content' : ''}{line.textColor ? ` ${line.textColor}` : ''}{line.backgroundColor ? ` ${line.backgroundColor}` : ''}"
		><code>{line.content}</code></pre>
	{/each}
</div>