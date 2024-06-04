<script>
	import { fade, fly } from 'svelte/transition';

	export let data;
</script>

{#if data?.country}
	{#key data.country}
		<div in:fade={{ duration: 1750 }} out:fly={{ y: 50 }}>
			<h2>{data.country}</h2>
			<h3>Population of {data.population.toLocaleString()} people</h3>
		</div>
	{/key}
{/if}

<style>
	div {
		position: absolute;
		bottom: -100px;
		right: 0;
		background: rgba(0, 0, 0, 0.75);
		padding: 1rem;
		border-radius: 0.5rem;
		text-align: right;
	}

	h2 {
		font-size: 1.5rem;
		font-weight: 600;
		margin-bottom: 0.5rem;
		letter-spacing: 3px;
		color: #eee;
	}

	h3 {
		font-size: 1rem;
		font-weight: 200;
		color: #ccc;
	}
</style>
