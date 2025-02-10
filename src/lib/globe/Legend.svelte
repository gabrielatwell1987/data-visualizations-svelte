<script>
	import { fade } from 'svelte/transition';

	export let data;
	export let colorScale;

	const minColor = colorScale.range()[0];
	const maxColor = colorScale.range()[1];
	const minValue = colorScale.domain()[0];
	const maxValue = colorScale.domain()[1];

	$: percentOfMax = (data?.population / maxValue) * 100;
</script>

<div class="legend">
	<span class="label">{minValue}</span>

	<div class="bar" style:background="linear-gradient(to right, {minColor} 0%, {maxColor} 100%)">
		{#if percentOfMax}
			<span class="line" style:left={percentOfMax + '%'} transition:fade></span>
		{/if}
	</div>

	<span class="label">{maxValue.toLocaleString()}</span>
</div>

<style>
	.legend {
		display: flex;
		gap: 6px;
		margin-top: 1rem;
	}

	.bar {
		position: relative;
		width: 100%;
		height: 15px;
	}

	.label {
		color: #ccc;
		font-size: 0.85rem;
		font-weight: 600;
		user-select: none;
	}

	.line {
		position: absolute;
		width: 2px;
		height: 15px;
		background: #ccc;
		transition: left 500ms cubic-bezier(1, 0, 0, 1);
	}
</style>
