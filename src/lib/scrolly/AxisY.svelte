<script>
	import { fade } from 'svelte/transition';

	export let yScale;
	export let width;

	let yTicks = yScale.ticks(4);
</script>

<g class="axis y">
	{#each yTicks as tick, i}
		<g class="tick" transform="translate(0 {yScale(tick)})" transition:fade={{ delay: i * 750 }}>
			<line x1="0" y1="0" x2={width} y2="0" stroke={i === 0 ? '#212121' : '#e5e7eb'} />
			<text x="0" y="-5">{tick} {i === yTicks.length - 1 ? ' hours studied' : ''}</text>
		</g>
	{/each}
</g>
