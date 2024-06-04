<script>
	import { fade } from 'svelte/transition';

	export let yScale;
	export let groupByContinent;

	const ticks = yScale.domain();
</script>

<g class="axis y">
	{#each ticks as tick, i}
		{#if groupByContinent}
			<g class="tick" in:fade={{ delay: i * 100 }} out:fade>
				<text x={0} y={yScale(tick)}>{tick}</text>
			</g>
		{/if}
	{/each}
</g>
