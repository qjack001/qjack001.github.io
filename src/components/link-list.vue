<template>
	<ul>
		<li v-for="(link, index) in links" :key="index">
			<a v-if="link.href" :href="link.href">
				{{ link.name }}
			</a>
			<template v-else>
				{{ link.name }}
			</template>
		</li>
	</ul>
</template>

<script>
	export default { 
		props: { 
			links: { 
				type: Array,
				default: () => [],
			},
		},
	}
</script>

<style scoped>
	a
	{
		color: var(--accent);
		text-decoration: none;
		outline: none;

		background-image: linear-gradient(var(--accent), var(--accent));
		background-size: 0% 1.6px;
		background-position: left bottom;
		background-repeat: no-repeat;

		transition: background-size 0.4s var(--ease);
	}

	a:hover,
	a:focus
	{
		background-size: 100% 1.6px;
	}

	ul
	{
		display: flex;
		align-items: flex-start;
		gap: 2.5ch;

		padding: 0;
		list-style: none;
	}

	li
	{
		animation: fade-up 2.5s var(--ease);
		animation-fill-mode: forwards;
		opacity: 0;
	}

	li:nth-child(1)
	{
		animation-delay: 0s;
	}

	li:nth-child(2)
	{
		animation-delay: 0.1s;
	}

	li:nth-child(3)
	{
		animation-delay: 0.25s;
	}

	li:nth-child(4)
	{
		animation-delay: 0.45s;
	}

	@media screen and (max-width: 740px)
	{
		a
		{
			background-size: 0% 2px;
		}

		a:hover,
		a:focus
		{
			background-size: 100% 2px;
		}

		ul
		{
			font-size: 1.4rem;
			gap: 3.5ch;
		}

		/* hack: homepage only */
		li:nth-child(4)
		{
			display: none;
		}
	}

	@media screen and (max-width: 500px)
	{
		ul
		{
			justify-content: space-between;
			gap: 0;
		}
	}

	@keyframes fade-up
	{
		0%
		{
			transform: translateY(100px);
			opacity: 0;
		}

		20%
		{
			opacity: 0;
		}

		100%
		{
			transform: translateY(0px);
			opacity: 1;
		}
	}
</style>