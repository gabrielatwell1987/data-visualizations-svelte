<script>
	import '../app.css';
	import Nav from '$lib/Nav.svelte';
	import Github from '$lib/Github.svelte';
</script>

<main>
	<div class="nav">
		<Nav />
	</div>

	<slot />

	<Github />
</main>

<style>
	:global(body) {
		color: #ccc;
		background-color: rgb(35, 35, 35);
	}

	main {
		& .nav {
			margin-bottom: 2em;
		}
	}
</style>
