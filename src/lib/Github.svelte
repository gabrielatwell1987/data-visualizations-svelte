<script>
</script>

<section>
	<h4>
		<a
			class="github"
			href="https://github.com/gabrielatwell1987/data-visualizations-svelte"
			target="_blank"><i class="fa-brands fa-github"></i></a
		>
	</h4>
</section>

<style>
	h4 {
		margin: 0;
		margin-top: 2%;

		& .github {
			position: fixed;
			bottom: 1rem;
			left: 1rem;
			text-decoration: none;
			color: #ccc;
			z-index: 5;

			& i {
				font-size: clamp(2em, 2vw, 5em);

				&:hover {
					color: rgba(179, 25, 25, 0.5);
				}
			}
		}
	}
</style>
