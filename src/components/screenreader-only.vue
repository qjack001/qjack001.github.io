<template>
	<div class="screenreader-only">
		<slot/>
	</div>
</template>

<style scoped>
	.screenreader-only
	{
		position: absolute !important;
		overflow: hidden;
		width: 1px;
		height: 1px;
		clip: rect(1px 1px 1px 1px);
		clip: rect(1px, 1px, 1px, 1px);
	}
</style>