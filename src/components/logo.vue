<template>
	<a :class="[ 'logo', fixed ? 'fixed' : '' ]" href="https://guinane.xyz">
		Jack Guinane
	</a>
</template>

<script>
	export default { 
		props: { 
			fixed: { 
				type: Boolean,
				default: () => false,
			},
		},
	}
</script>

<style scoped>
	.logo
	{
		background-color: var(--background);
		color: var(--foreground);
		text-decoration: none;
		text-align: center;
		outline: none;

		display: block;
		box-sizing: border-box;
		overflow: hidden;
		white-space: nowrap;

		position: absolute;
		top: 10px;

		transition: color 0.15s var(--ease);
		animation: expand 1.5s var(--ease) forwards;
		animation-delay: 2s;
		width: 0px;
		padding: 0px;
		left: 50%;
	}

	.logo.fixed
	{
		position: fixed;
		z-index: -90;
	}

	.logo:hover,
	.logo:focus
	{
		color: var(--accent);
	}

	@keyframes expand
	{
		from
		{
			width: 0px;
			padding: 0px;
			left: 50%;
		}

		to
		{
			width: 7rem;
			padding: 0 5px;
			left: calc(50% - 3.5rem);
		}
	}
</style>