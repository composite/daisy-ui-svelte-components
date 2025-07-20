<script lang="ts">
	interface Props {
		borderColor?:
			| 'primary'
			| 'secondary'
			| 'accent'
			| 'neutral'
			| 'info'
			| 'success'
			| 'warning'
			| 'error';
		class?: string;
		children?: any;
	}

	let { borderColor, class: className, children, ...restProps }: Props = $props();

	let classes = $derived(() => {
		let result = 'mockup-phone';

		if (borderColor) result += ` border-${borderColor}`;
		if (className) result += ` ${className}`;

		return result;
	});
</script>

<div class={classes()} {...restProps}>
	<div class="mockup-phone-camera"></div>
	<div class="mockup-phone-display">
		{@render children?.()}
	</div>
</div>
