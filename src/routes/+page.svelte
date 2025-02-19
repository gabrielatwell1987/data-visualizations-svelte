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
		font-family: var(--san-serif);
		font-size: clamp(1.25rem, 2vw, 3rem);
		font-weight: 600;
		color: #ccc;
		display: block;
	}

	h2 {
		text-align: center;
		font-family: var(--san-serif);
		font-size: clamp(1.2rem, 1.5vw, 1.75remrem);
		font-weight: 400;
		color: #ccc;
		margin-top: 5%;
		letter-spacing: 3px;
	}

	a {
		text-decoration: none;
		color: #ccc;
		cursor: pointer;

		& span {
			color: rgba(179, 25, 25, 0.75);
			font-family: var(--title-text);
			font-weight: 900;
			letter-spacing: 3px;
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
