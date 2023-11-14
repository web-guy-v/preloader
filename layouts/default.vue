<script setup>
</script>
<template>

	<div id="viewport">
		<ThePreloader />

		<slot />
	</div>

</template>
<style lang='scss'>

*,
*::before,
*::after {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}

body {
	background: #000;
	font-family: "anonymous-pro", monospace;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}

</style>