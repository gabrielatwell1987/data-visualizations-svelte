<script></script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css"
	/>
</svelte:head>

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
		font-weight: 400;
		font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
		color: #ccc;
		display: block;
	}

	h2,
	h4 {
		text-align: center;
		font-size: 1.25rem;
		font-weight: 200;
		font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
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
		font-size: 3rem;
	}

	span {
		color: rgb(179, 25, 25);
		font-weight: 900;
		letter-spacing: 5px;
		font-family: var(--san-serif);
	}

	a {
		text-decoration: none;
		color: #ccc;
	}

	i:hover {
		color: rgb(179, 25, 25);
	}
</style>
