<template>
	<div v-if="open" class="backdrop" @click="$emit('close')"></div>
	<transition name="modal">
		<dialog open v-if="open">
			<slot></slot>
		</dialog>
	</transition>
</template>

<script>
export default {
	props: ['open'],
	emits: ['close'],
};
</script>

<style lang="scss" scoped>
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
	box-shadow: 0 2px 8px rgb(255, 255, 255);
	background-color: white;
	/* animation: modal 0.5s ease-out forwards; */
}

// Modal animation
.modal-enter-active {
	// transition: all 0.3s ease-out;
	animation: modal 0.3s ease-out;
}

.modal-leave-active {
	// transition: all 0.3s ease-out;
	animation: modal 0.3s ease-in reverse;
}

@keyframes modal {
	from {
		opacity: 0;
		transform: translateY(-50px) scale(0.9);
	}

	to {
		opacity: 1;
		transform: translateY(0) scale(1);
	}
}
</style>