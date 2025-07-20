<script lang="ts">
	interface Props {
		url?: string;
		backgroundColor?: string;
		class?: string;
		children?: any;
	}

	let {
		url = 'https://daisyui.com',
		backgroundColor,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'mockup-browser';

		if (backgroundColor) result += ` ${backgroundColor}`;
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	<div class="mockup-browser-toolbar">
		<div class="input">{url}</div>
	</div>
	<div class="border-base-300 border-t">
		{@render children?.()}
	</div>
</div>
