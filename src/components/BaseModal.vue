<template>
	<div class="backdrop" @click="$emit('close')"></div>
	<dialog open>
		<slot></slot>
	</dialog>
</template>

<script>
export default {
	emits: ['close'],
};
</script>

<style scoped>
.backdrop {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100vh;
	z-index: 10;
	background-color: rgba(0, 0, 0, 0.75);
}

dialog {
	position: fixed;
	top: 30vh;
	left: calc(50% - 15rem);
	z-index: 100;
	width: 30rem;
	margin: 0;
	padding: 1rem;
	border: none;
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
	background-color: white;
}
</style>