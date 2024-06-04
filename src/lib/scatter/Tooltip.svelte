<script>
	import { fly } from 'svelte/transition';

	export let data;
	export let xScale;
	export let yScale;
	export let width;

	let tooltipWidth;
	let xNudge = 20;
	let yNudge = 20;

	$: x = xScale(data.grade);
	$: y = yScale(data.hours);
	$: xPosition = tooltipWidth + x > width ? x - tooltipWidth - xNudge : x + xNudge;
	$: yPosition = y + yNudge;
</script>

<main
	style="left: {xPosition}px; top: {yPosition}px;"
	bind:clientWidth={tooltipWidth}
	in:fly={{ y: -25, duration: 300 }}
	out:fly={{ y: 25, duration: 300 }}
>
	<h1>{data.name}: <span>{data.grade}%</span></h1>
	<h2>{data.hours} hours studied</h2>
</main>

<style>
	main {
		position: absolute;
		padding: 0.75rem;
		background: white;
		box-shadow: 2px 3px 8px rgba(0, 0, 0, 0.2);
		border-radius: 5px;
		pointer-events: none;
		transition:
			top 300ms ease,
			left 300ms ease;
	}

	h1 {
		font-size: 1rem;
		font-weight: 500;
		margin-bottom: 0.5rem;
		width: 100%;
	}

	h2 {
		font-size: 0.8rem;
		color: #8f8f8f;
		text-transform: uppercase;
		font-weight: 300;
	}

	span {
		font-size: 80%;
		padding: 2px 4px;
		background: rgba(65, 31, 31, 1);
		color: white;
		border-radius: 5px;
		margin-left: 0.25%;
		display: inline-block;
		vertical-align: bottom;
	}
</style>
