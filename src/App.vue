<template>
	<div class="container">
		<div class="block"></div>
		<button>Animate</button>
	</div>
	<base-modal @close="hideDialog" v-if="dialogIsVisible">
		<p>This is a test dialog!</p>
		<button @click="hideDialog">Close it!</button>
	</base-modal>
	<div class="container">
		<button @click="showDialog">Show Dialog</button>
	</div>
</template>  

<script>
export default {
	data() {
		return { dialogIsVisible: false };
	},
	methods: {
		showDialog() {
			this.dialogIsVisible = true;
		},
		hideDialog() {
			this.dialogIsVisible = false;
		},
	},
};
</script>

<style lang="scss">
* {
	box-sizing: border-box;
}
html {
	font-family: sans-serif;
}
body {
	margin: 0;
}

button {
	padding: 0.5rem 2rem;
	border: 1px solid transparent;
	border-radius: 12px;
	text-align: center;
	font: inherit;
	font-size: 17px;
	font-weight: 700;
	color: #000;
	text-decoration: none;
	background-color: #42b883;
	cursor: pointer;

	&:hover,
	&:active {
		background-color: #35495e;
		color: #fff;
	}
}

.container {
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
	max-width: 40rem;
	padding: 2rem;
	margin: 2rem auto;
	border-radius: 12px;
	box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);

	.block {
		width: 8rem;
		height: 8rem;
		margin-bottom: 2rem;
		background-color: #35495e;
	}
}
</style>