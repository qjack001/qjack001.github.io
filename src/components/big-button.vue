<template>
	<a
		:href="href"
		:class="[ 'bubble-button', dir ] "
	>
		<p aria-hidden="true" role="presentation">
			<slot/>
		</p>
		<screen-reader>
			<p>{{ text }}</p>
		</screen-reader>
		<div class="svg-container" role="presentation">
			<svg
				version="1.1"
				xmlns="http://www.w3.org/2000/svg"
				xmlns:xlink="http://www.w3.org/1999/xlink"
				x="0px" y="0px"
				width="300px" height="300px"
				viewBox="0 0 300 300"
				enable-background="new 0 0 300 300"
				xml:space="preserve"
			>
				<defs>
					<circle id="circlePath" cx="150"
						cy="150" r="50"
						fill="none"
					/>
				</defs>
				<g>
					<use xlink:href="#circlePath" fill="none"/>
					<text id="svg-text" fill="var(--accent)">
						<textPath xlink:href="#circlePath">
							{{ repeat(text) }}
						</textPath>
					</text>
				</g>
			</svg>
		</div>
	</a>
</template>

<script>
	import ScreenReader from './screenreader-only.vue'

	export default {
		components: { ScreenReader },

		props: { 
			text: { 
				type: String,
				default: () => '',
			},

			dir: { 
				type: String,
				default: () => 'right',
			},

			href: { 
				type: String,
				default: () => '',
			},
		},

		methods: {
			repeat: (text) => {
				let times = Math.ceil(48 / text.length)
				let textWithWhitespace = text + '\xa0\xa0\xa0' // non-breaking spaces
				return textWithWhitespace.repeat(times)
			},
		},
	}
</script>

<style scoped>
	.bubble-button
	{
		position: fixed;
		z-index: 99;
		width: 50px;
		height: 50px;
		top: 10px;

		cursor: pointer;
		text-decoration: none;
		text-align: center;

		background-color: var(--accent);
		border-radius: 100%;
		transform: rotate(10deg);
		transition: transform 0.4s var(--ease);
		animation: rotate-and-grow 2s var(--ease);
	}

	.bubble-button.left
	{
		left: 10px;
		position: absolute; /* hack: I only use fixed on home page */
	}

	.bubble-button.right
	{
		right: 10px;
	}

	.bubble-button:hover,
	.bubble-button:focus
	{
		transform: rotate(10deg) scale(1.8);
	}

	.bubble-button p
	{
		color: #fff;
		font-size: 2rem;
		margin: 0;
		line-height: 50px;
	}

	.bubble-button.left p
	{
		/* hack to make the back-arrow vertically aligned */
		line-height: 55px;
	}

	.bubble-button .svg-container
	{ 
		margin: 0%; 
		pointer-events: none;
		user-select: none;

		position: fixed;
		top: -240px;
		width: 400px;
		right: -170px;
		z-index: 99;

		transition: opacity 0.2s ease 0.05s;
		opacity: 0;
	}

	.bubble-button:hover .svg-container,
	.bubble-button:focus .svg-container
	{
		opacity: 1;
	}

	svg 
	{ 
		position: absolute; 
		left: 0; 
		top: 0;
		width: 100%; 
		height: 540px;

		animation: rotate-text 7s linear infinite;
	}

	#svg-text
	{
		font-family: var(--font);
		font-size: 0.75rem;
	}

	@keyframes rotate-text
	{
		from { transform: rotate(360deg) scale(0.8); }
		to   { transform: rotate(0) scale(0.8); }
	}

	@keyframes rotate-and-grow
	{
		from
		{
			opacity: 0;
			pointer-events: none;
			transform: rotate(-260deg) scale(0.1);
		}

		to
		{
			/* blocks hover state until animation is complete */
			pointer-events: none;
		}
	}
</style>