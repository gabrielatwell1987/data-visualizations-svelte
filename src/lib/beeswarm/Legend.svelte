<script>
	export let colorScale;
	export let hoveredContinent;

	const ticks = colorScale.domain();
</script>

<div
	class="legend"
	role="button"
	tabindex="0"
	on:mouseleave={() => {
		hoveredContinent = null;
	}}
>
	{#each ticks as continent}
		<span style="background-color: {colorScale(continent)}"></span>

		<p
			on:mouseover={() => {
				hoveredContinent = continent;
			}}
			on:focus={() => {
				hoveredContinent = continent;
			}}
			class:unhovered={hoveredContinent && hoveredContinent !== continent}
		>
			{continent}
		</p>
	{/each}
</div>

<style>
	.legend {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-wrap: wrap;
		gap: 5px 10px;
		margin-bottom: 2%;
	}

	span {
		display: inline-block;
		width: 20px;
		height: 20px;
		border-radius: 50%;
		border: 1px solid rgba(0, 0, 0, 0.5);
		margin-left: 1%;
	}

	span:first-child {
		margin-left: 0;
	}

	p {
		color: #8f8f8f;
		text-transform: uppercase;
		font-weight: 600;
		transition: opacity 300ms ease;
		font-size: 1rem;
		cursor: pointer;
	}

	.unhovered {
		opacity: 0.3;
	}
</style>
