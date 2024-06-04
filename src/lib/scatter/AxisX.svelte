<script>
	export let xScale;
	export let width;
	export let height;

	let xTicks = [0, 25, 50, 75, 100];
</script>

<g class="axis x" transform="translate(0 {height})">
	{#each xTicks as tick, i}
		<g class="tick" transform="translate({xScale(tick)}, 0)">
			<line x1="0" y1="0" x2="0" y2="6" stroke="hsla(212, 10%, 53%, 1)" />
			<text
				x={0}
				y={6}
				dy={10}
				dominant-baseline="middle"
				text-anchor={i === 0 ? 'start' : 'middle'}>{tick}%</text
			>
		</g>
	{/each}

	<text class="axis-title" x={width} y="0" dy="-5" dominant-baseline="start" text-anchor="end"
		>&larr; Final Grade &rarr;</text
	>
</g>
