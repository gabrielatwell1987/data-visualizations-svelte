<script>
	import AxisX from './AxisX.svelte';
	import AxisY from './AxisY.svelte';
	import Legend from './Legend.svelte';
	import Tooltip from './Tooltip.svelte';
	import data from '../../data/beeswarm.js';
	import { forceSimulation, forceX, forceY, forceCollide } from 'd3-force';
	import { scaleLinear, scaleBand, scaleOrdinal, scaleSqrt } from 'd3-scale';
	import { fade } from 'svelte/transition';

	let width = 400,
		height = 400;
	const margin = { top: 0, right: 0, left: 0, bottom: 50 };
	const RADIUS = 5;

	$: innerWidth = width - margin.left - margin.right;
	let innerHeight = height - margin.top - margin.bottom;

	import { mean, rollups } from 'd3-array';

	// Generate the average for each continent, so that we can sort according to that
	const continents = rollups(
		data,
		(v) => mean(v, (d) => d.happiness),
		(d) => d.continent
	) // Group data by continent and return the group-wide mean
		.sort((a, b) => a[1] - b[1]) // Sort according to value
		.map((d) => d[0]); // Grab the continent name

	const colorRange = ['#C40C0C', '#FF6500', '#FF8A08', '#FFC100', '#DD5746', '#8B322C'];

	let colorScale = scaleOrdinal()
		.domain(continents) // continents was already defined in our code
		.range(colorRange);

	$: radiusScale = scaleSqrt()
		.domain([1, 9]) // The same domain passed to xScale
		.range(width < 568 ? [2, 6] : [5, 10]);

	$: xScale = scaleLinear()
		.domain([1, 9]) // Alternatively, we could pass .domain(extent(data, d => d.happiness))
		.range([0, innerWidth]);

	let yScale = scaleBand().domain(continents).range([innerHeight, 0]).paddingOuter(0.5);

	let simulation = forceSimulation(data);
	let nodes = [];
	simulation.on('tick', () => {
		nodes = simulation.nodes();
	});

	$: {
		simulation
			.force(
				'x',
				forceX()
					.x((d) => xScale(d.happiness))
					.strength(0.8)
			)
			.force(
				'y',
				forceY()
					.y((d) => (groupByContinent ? yScale(d.continent) : innerHeight / 2))
					.strength(0.2)
			)
			.force(
				'collide',
				forceCollide().radius((d) => radiusScale(d.happiness))
			)
			.alpha(0.3) // [0, 1] The rate at which the simulation finishes. You should increase this if you want a faster simulation, or decrease it if you want more "movement" in the simulation.
			.alphaDecay(0.0005) // [0, 1] The rate at which the simulation alpha approaches 0. you should decrease this if your bubbles are not completing their transitions between simulation states.
			.restart();
	}

	let hovered;
	let hoveredContinent;
	let groupByContinent = false;
</script>

<h1>The Happiest Countries in the World</h1>

<Legend {colorScale} bind:hoveredContinent />

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
	class="chart-container"
	bind:clientWidth={width}
	on:click={() => {
		groupByContinent = !groupByContinent;
		hovered = null;
	}}
>
	<svg {width} {height}>
		{#if hovered}
			<line
				transition:fade
				x1={hovered.x}
				x2={hovered.x}
				y1={height - margin.bottom}
				y2={hovered.y + margin.top + radiusScale(hovered.happiness)}
				stroke={colorScale(hovered.continent)}
				stroke-width="5"
			/>
		{/if}
		<g
			class="inner-chart"
			transform="translate({margin.left}, {margin.top})"
			on:mouseleave={() => (hovered = null)}
			role="group"
		>
			<AxisX {xScale} height={innerHeight} width={innerWidth} />
			<AxisY {yScale} {groupByContinent} />
			{#each nodes as node, i}
				<circle
					in:fade={{ delay: 400 + i * 10 }}
					role="button"
					tabindex="0"
					cx={node.x}
					cy={node.y}
					r={radiusScale(node.happiness)}
					stroke={hovered || hoveredContinent
						? hovered === node || hoveredContinent === node.continent
							? '#eee'
							: 'transparent'
						: '#8f8f8f90'}
					stroke-width={hovered || hoveredContinent
						? hovered === node || hoveredContinent === node.continent
							? 2
							: 1
						: 1}
					fill={colorScale(node.continent)}
					title={node.country}
					opacity={hovered || hoveredContinent
						? hovered === node || hoveredContinent === node.continent
							? 1
							: 0.3
						: 1}
					on:mouseover={() => (hovered = node)}
					on:focus={() => (hovered = node)}
					on:click={(e) => {
						e.stopPropagation();
					}}
				/>
			{/each}
		</g>
	</svg>

	{#if hovered}
		<Tooltip data={hovered} {colorScale} {width} />
	{/if}
</div>

<style>
	:global(.tick text, .axis-title) {
		font-size: 12px;
		font-weight: 400;
		fill: hsla(212, 10%, 53%, 1);
		user-select: none;
	}

	h1 {
		margin: 3em 0 1.5rem 0;
		font-family: var(--san-serif);
		font-size: clamp(1.5rem, 3vw, 5rem);
		font-weight: 600;
		text-align: center;
		color: #eee;
		letter-spacing: 3px;

		@media (min-width: 500px) {
			margin: 0 0 1.5rem 0;
		}
	}

	circle {
		transition:
			stroke 300ms ease,
			opacity 300ms ease;
		cursor: pointer;
	}
</style>
