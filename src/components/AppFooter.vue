<template>
	<footer class="main-footer">
		<div class="container">
			<p>Very intresting tail</p>
		</div>
	</footer>
</template>

<script>
export default {
	props: {},
}
</script>

<style scoped>
.main-footer {
	position: relative;
	background: #222222;
	min-height: 221px;
}
.main-footer p {
	position: absolute;
	bottom: 0;
	right: 20px;
	color: #ffffff;
}
</style>
