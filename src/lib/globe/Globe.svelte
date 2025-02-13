<script>
	import world from '../../data/110m.json';
	import * as topojson from 'topojson-client';
	import { geoOrthographic, geoPath, geoCentroid } from 'd3-geo';
	import Glow from './Glow.svelte';
	import Tooltip from './Tooltip.svelte';
	import Legend from './Legend.svelte';
	import data from '../../data/globe.json';
	import { scaleLinear } from 'd3-scale';
	import { max } from 'd3-array';
	import { timer } from 'd3-timer';
	import { drag } from 'd3-drag';
	import { onMount } from 'svelte';
	import { select } from 'd3-selection';
	import { spring } from 'svelte/motion';
	import { draw } from 'svelte/transition';

	let countries = topojson.feature(world, world.objects.countries).features;
	let borders = topojson.mesh(world, world.objects.countries, (a, b) => a !== b);
	let width = 400;
	let xRotation = spring(0, { stiffness: 0.08, damping: 0.2 });
	let yRotation = spring(0, { stiffness: 0.08, damping: 0.5 });
	let degreesPerFrame = 0.1;
	let globe;
	let dragging = false;
	let tooltipData;

	const colorScale = scaleLinear()
		.domain([0, max(data, (d) => d.population)])
		.range(['#26362e', '#0dcc6c']);
	const t = timer((elapsed) => {
		if (dragging || tooltipData) return;
		$xRotation += degreesPerFrame;
	}, 0);
	const DRAG_SENSITIVITY = 2;

	$: height = width;
	$: projection = geoOrthographic()
		.scale(width / 2)
		.rotate([$xRotation, $yRotation])
		.translate([width / 2, height / 2]);
	$: path = geoPath(projection);
	$: if (tooltipData) {
		const center = geoCentroid(tooltipData);
		$xRotation = -center[0];
		$yRotation = -center[1];
	}

	countries.forEach((country) => {
		const metadata = data?.find((d) => d.id === country.id);

		if (metadata) {
			country.population = metadata.population;
			country.country = metadata.country;
		}
	});

	onMount(() => {
		const element = select(globe);

		element.call(
			drag()
				.on('drag', (event) => {
					$xRotation = $xRotation + event.dx / DRAG_SENSITIVITY;
					$yRotation = $yRotation - event.dy / DRAG_SENSITIVITY;
					dragging = true;
				})
				.on('end', () => {
					dragging = false;
				})
		);
	});
</script>

<div class="chart-container" bind:clientWidth={width}>
	<h1>To Glance at the World</h1>

	<h2>Population by country (2021)</h2>

	<svg {width} {height} bind:this={globe} class:dragging>
		<!-- glow effect -->
		<Glow />

		<!-- ocean -->
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-static-element-interactions -->
		<circle
			role="button"
			tabindex="0"
			cx={width / 2}
			cy={height / 2}
			r={width / 2}
			fill="#1c1c1c"
			stroke="none"
			filter="url(#glow)"
			on:click={() => {
				tooltipData = null;
			}}
			on:focus={() => {
				tooltipData = null;
			}}
		/>

		<!-- countries -->
		{#each countries as country}
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<path
				role="button"
				tabindex="0"
				d={path(country)}
				fill={colorScale(country?.population || 0)}
				stroke={'none'}
				on:click={() => {
					tooltipData = country;
				}}
				on:focus={() => {
					tooltipData = country;
				}}
			/>
		{/each}

		<!-- borders -->
		<path d={path(borders)} fill="none" stroke="black" />

		<!-- selected country -->
		{#if tooltipData}
			{#key tooltipData.id}
				<path
					d={path(tooltipData)}
					fill="transparent"
					stroke="#aaa"
					stroke-width="2"
					in:draw={{ duration: 1500 }}
				/>
			{/key}
		{/if}
	</svg>

	<Tooltip data={tooltipData} />

	<Legend {colorScale} data={tooltipData} />
</div>

<style>
	.chart-container {
		max-width: 468px;
		margin-inline: auto;
		margin-block: 5%;
	}

	svg {
		overflow: visible;
	}

	.dragging {
		cursor: grabbing;
	}

	path {
		cursor: pointer;
	}

	path:focus {
		outline: none;
	}

	h1,
	h2 {
		color: antiquewhite;
		text-align: center;
	}

	h1 {
		font-family: 'Roboto Condensed', sans-serif;
		font-size: 2rem;
		font-weight: 700;
		margin-top: 2em;
		margin-bottom: 5%;
		letter-spacing: 1px;
		font-family: var(--mono);

		@media (min-width: 500px) {
			margin-top: 0;
		}
	}

	h2 {
		font-family: 'Roboto Condensed', sans-serif;
		font-size: 1.25rem;
		font-weight: 200;
		margin-bottom: 7.5%;
	}
</style>
