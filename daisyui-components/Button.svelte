<script lang="ts" module>
	import type { SvelteHTMLElements } from 'svelte/elements';

	const colors = {
		neutral: 'btn-neutral',
		primary: 'btn-primary',
		secondary: 'btn-secondary',
		accent: 'btn-accent',
		info: 'btn-info',
		success: 'btn-success',
		warning: 'btn-warning',
		error: 'btn-error'
	} as const;
	const variants = {
		outline: 'btn-outline',
		dash: 'btn-dash',
		soft: 'btn-soft',
		ghost: 'btn-ghost',
		link: 'btn-link'
	} as const;
	const sizes = {
		xs: 'btn-xs',
		sm: 'btn-sm',
		md: 'btn-md',
		lg: 'btn-lg',
		xl: 'btn-xl'
	} as const;
	const shapes = {
		square: 'btn-square',
		circle: 'btn-circle'
	};
	type HrefCond = Required<Pick<SvelteHTMLElements['a'], 'href'>>;
	type ButtonOrAnchor<T extends ButtonOrAnchorAttributes> = T extends HrefCond
		? HTMLAnchorElement
		: HTMLButtonElement;
	type ButtonOrAnchorAttributes =
		| (Omit<SvelteHTMLElements['a'], 'href' | 'type'> &
				HrefCond & {
					type?: never;
					disabled?: SvelteHTMLElements['button']['disabled'];
				})
		| (SvelteHTMLElements['button'] & { href?: never });
	type ButtonProps = {
		color?: keyof typeof colors;
		size?: keyof typeof sizes;
		variant?: keyof typeof variants;
		shape?: keyof typeof shapes;
		loading?: boolean;
		wide?: boolean;
		block?: boolean;
		active?: boolean;
	};
</script>

<script lang="ts">
	import type { RefElement } from '$components/ui/index';
	import { cn } from '$lib/utils/doms';

	let {
		color,
		size,
		variant,
		shape,
		loading = false,
		wide = false,
		block = false,
		active = false,
		class: className,
		children,
		href,
		disabled,
		type,
		ref = $bindable(null),
		...restProps
	}: ButtonOrAnchorAttributes &
		ButtonProps &
		RefElement<ButtonOrAnchor<ButtonOrAnchorAttributes>> = $props();

	let classes = $derived(
		cn(
			'btn',
			color && colors[color],
			size && sizes[size],
			shape && shapes[shape],
			variant && variants[variant],
			wide && 'btn-wide',
			block && 'btn-block',
			active && 'btn-active',
			className
		)
	);
</script>

<svelte:element
	this={href ? 'a' : 'button'}
	class={classes}
	href={href && !disabled && !loading ? href : undefined}
	type={href ? undefined : type}
	disabled={href ? undefined : disabled || loading}
	aria-disabled={href ? disabled : undefined}
	role={href && disabled ? 'link' : undefined}
	tabindex={href && (disabled || loading) ? -1 : 0}
	bind:this={ref}
	{...restProps}
>
	{#if loading}
		<span class="loading loading-spinner"></span>
	{/if}
	{@render children?.()}
</svelte:element>
