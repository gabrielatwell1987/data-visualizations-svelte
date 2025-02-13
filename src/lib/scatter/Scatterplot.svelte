<script>
	import data from '../../data/scatter.js';
	import { scaleLinear } from 'd3-scale';
	import AxisX from './AxisX.svelte';
	import AxisY from './AxisY.svelte';
	import Tooltip from './Tooltip.svelte';
	import { fade } from 'svelte/transition';

	const margin = {
		top: 20,
		right: 20,
		bottom: 20,
		left: 0
	};

	let width = 400;
	let height = 400;
	let hoveredData;

	$: innerWidth = width - margin.left - margin.right;
	$: innerHeight = height - margin.top - margin.bottom;
	$: xScale = scaleLinear().domain([0, 100]).range([0, innerWidth]);
	$: yScale = scaleLinear().domain([0, 60]).range([innerHeight, 0]);
</script>

<h1>Students</h1>

<div class="chart-container" bind:clientWidth={width} in:fade={{ duration: 1000 }}>
	<svg {width} {height}>
		<g transform="translate({margin.left} {margin.top})">
			<AxisX {xScale} height={innerHeight} width={innerWidth} />
			<AxisY {yScale} width={innerWidth} />
			{#each data.sort((a, b) => a.grade - b.grade) as d}
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
					on:mouseover={() => (hoveredData = d)}
					on:focus={() => (hoveredData = d)}
					on:mouseleave={() => (hoveredData = null)}
				/>
			{/each}
		</g>
	</svg>
	{#if hoveredData}
		<Tooltip data={hoveredData} {xScale} {yScale} width={innerWidth} />
	{/if}
</div>

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
			opacity 500ms ease;
	}

	h1 {
		font-size: 2.5rem;
		font-weight: 600;
		margin-bottom: 1rem;
		margin-top: 2em;
		letter-spacing: 5px;
		color: #eee;
		text-align: center;
		font-family: 'Roboto Condensed', sans-serif;

		@media (min-width: 500px) {
			margin-top: 0;
		}
	}
</style>
