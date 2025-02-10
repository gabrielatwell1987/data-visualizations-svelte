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
		background-color: rgb(40, 40, 40);
	}
</style>
