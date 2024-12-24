<script></script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css"
	/>
</svelte:head>

<article>
	<main>
		<h1>This is from the <span>Better Data Visualization</span> course.</h1>
	</main>

	<h2>These are different charts that I made with svelte and d3 and random data...</h2>

	<section>
		<h3>Here is the github repo</h3>

		<h4>
			<a href="https://github.com/gabrielatwell1987/data-visualizations-svelte"
				><i class="fa-brands fa-github"></i></a
			>
		</h4>
	</section>
</article>

<style>
	main {
		display: flex;
		justify-content: center;
		align-items: center;
		margin-block: 10%;
		position: relative;
	}

	h1,
	h3 {
		text-align: center;
		font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
			sans-serif;
		font-size: clamp(1.25rem, 2vw, 3rem);
		font-weight: 400;
		color: #ccc;
		display: block;
	}

	h2,
	h4 {
		text-align: center;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
		font-size: clamp(1.2rem, 2vw, 2rem);
		font-weight: 200;
		color: #ccc;
		margin-top: 5%;
		letter-spacing: 3px;
	}

	h3 {
		margin-top: 5%;
	}

	h4 {
		margin: 0;
		margin-top: 2%;
	}

	span {
		color: rgb(179, 25, 25);
		font-family: var(--mono);
		font-weight: 900;
		letter-spacing: 5px;
	}

	a {
		text-decoration: none;
		color: #ccc;
	}

	i {
		font-size: 8rem;

		&:hover {
			color: rgb(179, 25, 25);
		}
	}

	@media (min-width: 300px) {
		main {
			padding: 0.5rem;
		}

		article {
			padding: 1rem;
		}
	}
</style>
