<script>
	import '../app.css';
	import Nav from '$lib/Nav.svelte';
</script>

<main>
	<Nav />
	<slot></slot>
</main>

<style>
	:global(body) {
		background-color: rgb(40, 40, 40);
	}
</style>
