<script lang="ts">
	interface Props {
		src?: string;
		alt?: string;
		size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl' | number;
		shape?: 'circle' | 'rounded' | 'square';
		online?: boolean;
		offline?: boolean;
		placeholder?: string;
		ring?: boolean;
		ringColor?: string;
		class?: string;
		children?: any;
	}

	let {
		src,
		alt = 'Avatar',
		size = 'md',
		shape = 'circle',
		online = false,
		offline = false,
		placeholder,
		ring = false,
		ringColor,
		class: className,
		children,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'avatar';
		
		if (online) result += ' avatar-online';
		if (offline) result += ' avatar-offline';
		if (placeholder) result += ' placeholder';
		if (className) result += ` ${className}`;
		
		return result;
	});

	let innerClasses = $derived(() => {
		let result = '';
		
		// Size classes
		if (typeof size === 'number') {
			result += `w-${size} h-${size}`;
		} else {
			const sizeMap = {
				xs: 'w-6 h-6',
				sm: 'w-8 h-8', 
				md: 'w-12 h-12',
				lg: 'w-16 h-16',
				xl: 'w-20 h-20'
			};
			result += sizeMap[size];
		}
		
		// Shape classes
		if (shape === 'circle') result += ' rounded-full';
		else if (shape === 'rounded') result += ' rounded';
		else if (shape === 'square') result += ' rounded-none';
		
		// Ring classes
		if (ring) {
			result += ' ring ring-offset-base-100 ring-offset-2';
			if (ringColor) result += ` ring-${ringColor}`;
		}
		
		return result;
	});
</script>

<div class={classes()} {...restProps}>
	<div class={innerClasses()}>
		{#if src}
			<img {src} {alt} />
		{:else if placeholder}
			<span class="text-xl">{placeholder}</span>
		{:else if children}
			{@render children()}
		{/if}
	</div>
</div>