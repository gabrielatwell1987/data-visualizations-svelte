<script></script>

<section>
	<p>
		This is from a tutorial I took on to learn with Svelte and D3. I learned how to make a
		scrollytelling, which is a way to tell a story.
	</p>

	<p>
		D3 and svelte together are a powerful combination. They allow you to create dynamic and
		interactive data visualizations.
	</p>

	<p>
		Data visualization is a way to communicate information clearly and effectively through graphical
		means. It is a way to make sense of data and to see patterns and trends that might not be
		apparent in raw data.
	</p>

	<p>
		The creator of svelte, Rich Harris, worked for the NY Times as a data visualization engineer. He
		has a great tutorial on how to use svelte and d3 together. I highly recommend it.
	</p>
</section>

<style>
	section {
		margin-top: 5%;
		max-width: 75%;
		margin-inline: auto;
	}

	p:not(:last-of-type) {
		margin-bottom: 1rem;
	}

	p {
		font-size: 1.25rem;
		letter-spacing: 3px;
		line-height: 1.75rem;
		color: #ccc;
	}

	@media (min-width: 300px) {
		p {
			font-size: 1rem;
			line-height: 1.25;
		}

		section {
			max-width: 95%;
		}
	}

	@media (min-width: 600px) {
		p {
			font-size: 1.25rem;
			line-height: 1.5;
		}

		section {
			max-width: 90%;
		}
	}

	@media (min-width: 800px) {
		p {
			font-size: 1.5rem;
			line-height: 1.75;
			font-weight: 600;
		}
	}
</style>
