<script>
	import '../app.css';
	import Nav from '$lib/Nav.svelte';
	import Github from '$lib/Github.svelte';
</script>

<main>
	<Nav />

	<slot />

	<Github />
</main>

<style>
	:global(body) {
		color: #ccc;
		background-color: rgb(35, 35, 35);
	}
</style>
