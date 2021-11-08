<template>
	<screen-reader>
		<h1>About me</h1>
	</screen-reader>
	<big-text animate>
		<p class="outline">
			I’m <strong>Jack Guinane</strong>, a developer with big dreams making little websites.
		</p>
	</big-text>
	<link-list
		:links="[
			{ name: 'Github', href: 'https://github.com/qjack001' },
			{ name: 'Resume', href: 'https://guinane.xyz/Resume.pdf' },
			{ name: 'Email', href: 'mailto:jackguinane@gmail.com' },
			{ name: 'or scroll down to see what I’ve been working on.' },
		]"
	/>
</template>

<script>
	import ScreenReader from './screenreader-only.vue'
	import BigText from './big-text.vue'
	import LinkList from './link-list.vue'

	export default {
		components: {
			ScreenReader,
			BigText,
			LinkList,
		},
	}
</script>

<style scoped>
	.outline strong
	{
		color: var(--foreground);
		-webkit-text-stroke-width: 0px;
		-webkit-text-stroke-color: transparent;
		font-size: 1.1em;
	}
</style>