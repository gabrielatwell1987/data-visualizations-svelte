<script>
	import data from '../../data/scatter.js';
	import { scaleLinear } from 'd3-scale';
	import AxisX from './AxisX.svelte';
	import AxisY from './AxisY.svelte';
	import Tooltip from './Tooltip.svelte';
	import { fade } from 'svelte/transition';
	import Telling from '../../helpers/Telling.svelte';
	import Text from './Text.svelte';

	const margin = {
		top: 20,
		right: 20,
		bottom: 20,
		left: 0
	};

	let currentStep;
	let width = 400;
	let height = 400;
	let hoveredData;
	let initialData = data.sort((a, b) => a.grade - b.grade);
	let renderedData = initialData;

	$: innerWidth = width - margin.left - margin.right;
	$: innerHeight = height - margin.top - margin.bottom;
	$: xScale = scaleLinear().domain([0, 100]).range([0, innerWidth]);
	$: yScale = scaleLinear().domain([0, 60]).range([innerHeight, 0]);
	$: xMidpoint = (xScale.domain()[1] + xScale.domain()[0]) / 2;
	$: yMidpoint = (yScale.domain()[1] + yScale.domain()[0]) / 2;
	$: {
		if (currentStep === 0) {
			renderedData = initialData.map((d) => ({ ...d, grade: xMidpoint, hours: yMidpoint }));
			hoveredData = null;
		} else if (currentStep === 1) {
			renderedData = initialData.map((d) => ({ ...d, hours: yMidpoint }));
			hoveredData = null;
		} else if (currentStep === 2) {
			renderedData = initialData;
			hoveredData = renderedData[5];
		}
	}
</script>

<h1>Scroll down!</h1>

<Text />

<section>
	<div class="sticky">
		<div
			class="chart-container"
			bind:clientWidth={width}
			bind:clientHeight={height}
			in:fade={{ duration: 1000 }}
		>
			<svg {width} {height}>
				<g transform="translate({margin.left} {margin.top})">
					{#if currentStep > 0}
						<AxisX {xScale} height={innerHeight} width={innerWidth} />
					{/if}

					{#if currentStep > 1}
						<AxisY {yScale} width={innerWidth} />
					{/if}

					{#each renderedData as d}
						<circle
							role="button"
							tabindex="0"
							cx={xScale(d.grade)}
							cy={yScale(d.hours)}
							r={hoveredData === d ? 20 : 10}
							opacity={hoveredData ? (hoveredData === d ? 1 : 0.5) : 1}
							fill="darkred"
							stroke="#8f8f8f"
							stroke-width="2"
							on:mouseover={() => {
								if (currentStep < 1) return;
								hoveredData = d;
							}}
							on:focus={() => {
								if (currentStep < 1) return;
								hoveredData = d;
							}}
							on:mouseleave={() => (hoveredData = null)}
						/>
					{/each}
				</g>
			</svg>
			{#if hoveredData}
				<Tooltip data={hoveredData} {xScale} {yScale} width={innerWidth} />
			{/if}
		</div>
	</div>

	<div class="steps">
		<Telling bind:value={currentStep}>
			{#each ['made', 'with', 'svelte'] as text, i}
				<div class="step" class:active={currentStep === i}>
					<div class="step-content">
						<div class="step-content">
							<p><b>{text}</b></p>
						</div>
					</div>
				</div>
			{/each}
		</Telling>
	</div>
</section>

<Text />

<style>
	:global(.tick text, .axis-title) {
		font-weight: 600;
		font-size: 1rem;
		fill: #8f8f8f;
	}

	svg {
		margin-top: 2%;
	}

	circle {
		cursor: pointer;
		transition:
			r 300ms ease,
			opacity 500ms ease,
			cx 500ms cubic-bezier(0.76, 0, 0.24, 1),
			cy 500ms cubic-bezier(0.76, 0, 0.24, 1);
	}

	h1 {
		font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
		font-size: 2.5rem;
		font-weight: 600;
		margin-top: 3%;
		margin-bottom: 1rem;
		letter-spacing: 5px;
		color: #eee;
		text-align: center;
	}

	b {
		letter-spacing: 3px;
	}

	.step {
		height: 90vh;
		opacity: 0.3;
		transition: opacity 500ms ease;
		display: flex;
		justify-content: center;
		place-items: center;
	}

	.step.active {
		opacity: 1;
	}

	.step-content {
		background-color: #eee;
		padding: 0.75rem 1rem;
		border-radius: 5px;
	}

	section {
		position: relative;
	}

	.sticky {
		position: sticky;
		top: 0;
		z-index: 1;
		height: 90vh;
		margin-bottom: 2%;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.steps {
		position: relative;
		z-index: 2;
		pointer-events: none;
	}

	.chart-container {
		max-width: 1000px;
		max-height: 500px;
		margin-inline: auto;
		width: 100%;
		height: 100%;
	}
</style>
