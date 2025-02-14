<script>
	import Title from '$lib/Title.svelte';

	let isMenuOpen = false;

	const toggleMenu = () => {
		isMenuOpen = !isMenuOpen;
	};
</script>

<nav>
	<a href="/">
		<img src="graph.png" alt="" />

		<Title />
	</a>

	<button class="hamburger" on:click={toggleMenu} aria-label="Menu">
		<span></span>
		<span></span>
		<span></span>
	</button>

	<ul class:active={isMenuOpen}>
		<li>
			<h1>
				<a href="/scatter">Scatterplot</a>
			</h1>
		</li>

		<li>
			<h1>
				<a href="/beeswarm">Beeswarm</a>
			</h1>
		</li>

		<li>
			<h1>
				<a href="/globe">Globe</a>
			</h1>
		</li>

		<li>
			<h1>
				<a href="/scrolly">Scrolly</a>
			</h1>
		</li>
	</ul>
</nav>

<style>
	nav {
		background-color: #111;
		display: flex;
		align-items: center;
		justify-content: space-evenly;
		margin-bottom: 3%;
		border-bottom: 20px double rgba(35, 35, 35, 1);

		& ul {
			display: flex;
			justify-content: center;
			align-items: center;
			list-style-type: none;
			gap: 3rem;

			& li {
				transition: transform 0.5s ease;
				margin: 0;

				&:hover {
					transform: scale(1.05);
				}

				& h1 a {
					font-size: clamp(1.25rem, 2vw, 3rem);
					margin: 0;
					padding: 0;
					transition: color 0.5s ease;

					&:hover {
						color: rgba(179, 25, 25, 0.5);
					}
				}
			}
		}

		& a {
			color: #eee;
			text-decoration: none;
			font-size: clamp(1.5rem, 2vw, 3rem);
			letter-spacing: 2px;
			display: flex;
			align-items: center;
			justify-content: center;
			gap: 2rem;
			margin-left: 1rem;
			margin-right: 1rem;

			& img {
				width: clamp(em, 2vw, 5em);
				height: clamp(3em, 2vw, 5em);
				transition: transform 0.5s ease;
				margin-left: 15rem;

				&:hover {
					transform: scale(1.05);
				}

				@media (max-width: 500px) {
					display: none;
				}
			}
		}
	}

	.hamburger {
		display: none;
		flex-direction: column;
		justify-content: space-around;
		width: 2rem;
		height: 2rem;
		background: transparent;
		border: none;
		cursor: pointer;
		padding: 0;
		z-index: 10;

		& span {
			width: 2rem;
			height: 0.25rem;
			background: #eee;
			border-radius: 10px;
			transition: all 0.3s linear;
			position: relative;
			transform-origin: 1px;
		}
	}

	@media (max-width: 799px) {
		.hamburger {
			display: flex;
			position: absolute;
			right: 2rem;
			top: 50%;
			transform: translateY(-50%);
			z-index: 11;
		}

		ul {
			position: fixed;
			inset: 0;
			min-height: 100vh;
			width: 100%;
			background: #111;
			padding: 0;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			gap: 0.1rem;
			transform: translateX(-100%);
			transition: transform 0.5s ease-in-out;
			z-index: 5;
			margin: 0;
		}

		ul li {
			text-align: center;
			width: 100%;
		}

		ul li h1 {
			margin: 1rem 0;
		}

		ul.active {
			transform: translateX(0);
		}

		nav {
			padding: 1rem;
			width: 100%;
			position: fixed;
			top: 0;
			left: 0;
			z-index: 10;
			height: 4rem;
		}

		img {
			display: none;
		}

		a {
			/* font-size: clamp(1.5rem, 2vw, 3rem); */
			margin-right: 1rem;
		}
	}

	@media (min-width: 300px) {
		img {
			display: none;
		}

		ul {
			margin-inline: auto;
			/* gap: 0.25rem; */
		}

		li {
			margin-inline: auto;
		}

		a {
			/* font-size: clamp(1.5rem, 2vw, 2.5rem); */
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
			display: flex;
			flex-direction: row;
			justify-content: center;
			align-items: center;
			gap: 1.5rem;
			width: auto;
			position: static;
			transform: none;
			height: auto;
			padding: 0;
		}

		.hamburger {
			display: none;
		}

		img {
			display: block;
		}
	}
</style>
