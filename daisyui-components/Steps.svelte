<script lang="ts">
	interface Step {
		id: string;
		label: string;
		completed?: boolean;
		color?:
			| 'neutral'
			| 'primary'
			| 'secondary'
			| 'accent'
			| 'info'
			| 'success'
			| 'warning'
			| 'error';
	}

	interface Props {
		steps: Step[];
		direction?: 'horizontal' | 'vertical';
		class?: string;
	}

	let { steps, direction = 'horizontal', class: className, ...restProps }: Props = $props();

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
		<li
			class="step{step.completed
				? step.color === 'neutral'
					? ' step-neutral'
					: step.color === 'primary'
						? ' step-primary'
						: step.color === 'secondary'
							? ' step-secondary'
							: step.color === 'accent'
								? ' step-accent'
								: step.color === 'info'
									? ' step-info'
									: step.color === 'success'
										? ' step-success'
										: step.color === 'warning'
											? ' step-warning'
											: step.color === 'error'
												? ' step-error'
												: ' step-primary'
				: ''}"
		>
			{step.label}
		</li>
	{/each}
</ul>
