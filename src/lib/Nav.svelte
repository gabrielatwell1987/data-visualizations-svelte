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
		padding: 1rem;
		display: flex;
		align-items: center;
		justify-content: space-evenly;
		margin-bottom: 1%;
	}

	ul {
		display: flex;
		justify-content: space-evenly;
		list-style-type: none;
		margin: 0;
		padding: 0;
		gap: 1.5rem;
	}

	li {
		margin: 0 1rem;
		transition: transform 0.5s ease;
	}

	li:hover {
		transform: scale(1.05);
	}

	a {
		color: #eee;
		text-decoration: none;
		font-size: 1.5rem;
		letter-spacing: 2px;
	}

	img {
		width: 200px;
		height: 75px;
		transition: transform 0.5s ease;
	}

	img:hover {
		transform: scale(1.05);
	}

	@media (min-width: 300px) {
		img {
			display: none;
		}

		ul {
			flex-direction: column;
		}

		li {
			margin: 0;
			margin-inline: auto;
		}

		h1 {
			font-size: 1rem;
		}
	}

	@media (min-width: 600px) {
		nav {
			width: 100%;
		}

		/* ul {
			flex-direction: row;
		} */

		h1 {
			font-size: 1.25rem;
		}

		img {
			display: block;
		}
	}

	@media (min-width: 800px) {
		nav {
			width: 100%;
		}

		ul {
			flex-direction: row;
		}

		h1 {
			font-size: 1.75rem;
		}
	}
</style>
