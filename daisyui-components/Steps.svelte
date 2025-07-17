<script lang="ts">
	interface Step {
		id: string;
		label: string;
		completed?: boolean;
		color?: 'neutral' | 'primary' | 'secondary' | 'accent' | 'info' | 'success' | 'warning' | 'error';
	}

	interface Props {
		steps: Step[];
		direction?: 'horizontal' | 'vertical';
		class?: string;
	}

	let {
		steps,
		direction = 'horizontal',
		class: className,
		...restProps
	}: Props = $props();

	let classes = $derived(() => {
		let result = 'steps';
		
		if (direction === 'vertical') result += ' steps-vertical';
		if (direction === 'horizontal') result += ' steps-horizontal';
		if (className) result += ` ${className}`;
		
		return result;
	});
</script>

<ul class={classes()} {...restProps}>
	{#each steps as step (step.id)}
		<li class="step{step.completed ? ` step-${step.color || 'primary'}` : ''}">
			{step.label}
		</li>
	{/each}
</ul>