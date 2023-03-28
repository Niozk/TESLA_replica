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
		padding: 14px 0;
		border: 0;
		border-radius: 5px;
		width: 300px;
		white-space: nowrap;
		font-size: 16px;
		font-family: inherit;
		font-weight: bold;
		cursor: pointer;
		color: v-bind(color);
		background-color: v-bind(backgroundColor);
	}
</style>