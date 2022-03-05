<template>
	<div class="formatted-markdown">
		<slot/>
	</div>
</template>

<!-- eslint-disable-next-line vue-scoped-css/enforce-style-type -->
<style>
	@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@500&display=swap');

	.formatted-markdown
	{
		display: grid;
		grid-template-columns:  1fr minmax(0, 60ch) 1fr;

		font-size: 24px;
		line-height: 1.5;
	}

	.formatted-markdown *
	{
		grid-column: 2;
	}

	.formatted-markdown img,
	.formatted-markdown video
	{
		grid-column: 1 / -1;

		max-width: 100%;
		max-height: 700px;
		object-fit: contain;

		border-radius: 10px;
		margin: 2em auto;
	}

	.formatted-markdown p
	{
		margin: 1.5em 0;
	}

	.formatted-markdown a
	{
		color: currentColor;
		text-decoration: none;
		background-image: linear-gradient(currentColor, currentColor);
		background-size: 100% 0.07em;
		background-position: left bottom;
		background-repeat: no-repeat;
	}

	.formatted-markdown code
	{
		font-family: "IBM Plex Mono", monospace;
		font-size: 95%;
		padding: 0.1em 0.4em;
		border-radius: 10px;
		background: var(--almost-white-blue);
	}

	.formatted-markdown pre code
	{
		display: block;
		overflow-x: scroll;
		padding: 1ch 2ch;
		font-size: 18px;
		tab-size: 4ch;
	}
	
	@media screen and (max-width: 740px)
	{
		.formatted-markdown
		{
			font-size: 18px;
		}
	}
</style>