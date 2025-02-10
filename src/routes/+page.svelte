<script></script>

<svelte:head>
	<link
		rel="stylesheet"
		href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css"
	/>
</svelte:head>

<article>
	<main>
		<h1>
			This is from the <a
				href="https://www.newline.co/courses/better-data-visualizations-with-svelte"
				target="_blank"><span>Better Data Visualization</span></a
			> course.
		</h1>

		<h2>These are different charts that I made with svelte and d3 and random data...</h2>
	</main>

	<section>
		<h4>
			<a
				class="github"
				href="https://github.com/gabrielatwell1987/data-visualizations-svelte"
				target="_blank"><i class="fa-brands fa-github"></i></a
			>
		</h4>
	</section>
</article>

<style>
	main {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin-block: 10%;
		position: relative;
	}

	h1 {
		text-align: center;
		font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
			sans-serif;
		font-size: clamp(1.25rem, 2vw, 3rem);
		font-weight: 400;
		color: #ccc;
		display: block;
	}

	h2 {
		text-align: center;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
		font-size: clamp(1.2rem, 2vw, 2rem);
		font-weight: 200;
		color: #ccc;
		margin-top: 5%;
		letter-spacing: 3px;
	}

	h4 {
		margin: 0;
		margin-top: 2%;
	}

	.github {
		position: absolute;
		bottom: 1rem;
		left: 1rem;
	}

	a {
		text-decoration: none;
		color: #ccc;
		cursor: pointer;

		& span {
			color: rgba(179, 25, 25, 0.75);
			font-family: var(--san-serif);
			font-weight: 900;
			letter-spacing: 5px;
		}
	}

	i {
		font-size: clamp(1.2rem, 3vw, 5rem);

		&:hover {
			color: rgba(179, 25, 25, 0.5);
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
