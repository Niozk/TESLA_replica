<template>
    <button>{{ text }}</button>
</template>

<script setup>
	const props = defineProps({
		text: String,
		color: String,
		backgroundColor: String
	})
</script>

<style scoped>
	button {
		padding: 11px 0;
		margin: 0 14px;
		width: 260px;
		white-space: nowrap;
		border: 0;
		border-radius: 5px;
		font-size: 14px;
		font-family: inherit;
		font-weight: bold;
		cursor: pointer;
		color: v-bind(color);
		background-color: v-bind(backgroundColor);
	}
</style>