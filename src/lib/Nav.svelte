<script></script>

<nav>
	<a href="/"><img src="graph.png" alt="" /></a>

	<ul>
		<li><h1><a href="/scatter">Scatterplot</a></h1></li>
		<li><h1><a href="/beeswarm">Beeswarm</a></h1></li>
		<li><h1><a href="/globe">Globe</a></h1></li>
		<li><h1><a href="/scrolly">Scrolly</a></h1></li>
	</ul>
</nav>

<style>
	nav {
		background-color: #111;
		display: flex;
		align-items: center;
		justify-content: space-evenly;
		margin-bottom: 3%;
	}

	ul {
		display: flex;
		justify-content: space-evenly;
		list-style-type: none;
		gap: 1.5rem;
	}

	li {
		margin: 0 1rem;
		transition: transform 0.5s ease;

		&:hover {
			transform: scale(1.05);
		}
	}

	a {
		color: #eee;
		text-decoration: none;
		font-size: 1.5rem;
		letter-spacing: 2px;
	}

	img {
		width: 200px;
		height: 200px;
		transition: transform 0.5s ease;
		margin-left: 15rem;

		&:hover {
			transform: scale(1.05);
		}
	}

	@media (min-width: 300px) {
		img {
			display: none;
		}

		ul {
			flex-direction: column;
			margin-inline: auto;
			gap: 0.25rem;
		}

		li {
			margin-inline: auto;
		}

		a {
			font-size: clamp(1.5rem, 2vw, 3rem);
			margin-right: 1rem;
		}

		nav {
			padding: 1rem;
		}
	}

	@media (min-width: 600px) {
		nav {
			width: 100%;
		}

		img {
			display: block;
		}

		ul {
			gap: 1rem;
		}
	}

	@media (min-width: 800px) {
		nav {
			width: 100%;
			padding: 0;
		}

		ul {
			flex-direction: row;
			gap: 1.5rem;
		}
	}
</style>
