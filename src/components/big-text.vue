<template>
	<!-- TODO: make animate optional (prop) -->
	<span class="slotted animate">
		<slot/>
	</span>
</template>

<style scoped>
	.slotted
	{
		font-size: var(--text-xl);
		font-weight: bold;
		line-height: 1.3;

		display: block;
		transform: translateY(0px) scaleY(1);
		transform-origin: top;
		opacity: 1;
		z-index: 99;
	}

	.slotted.animate
	{
		animation: entry-animation 2s var(--ease);
	}

	.slotted h1
	{
		font-size: 1em;
	}

	@keyframes entry-animation
	{
		0%
		{
			transform: translateY(100px) scaleY(1.7);
			opacity: 0;
		}

		20%
		{
			opacity: 0;
		}
	}
</style>