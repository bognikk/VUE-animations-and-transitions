<template>
	<router-view v-slot="slotProps">
		<transition name="fade-button" mode="out-in">
			<component :is="slotProps.Component"></component>
		</transition>
	</router-view>
	<router-view>
		<div v-if="usersAreVisible" class="container">
			<h5>animated lists</h5>
			<users-list></users-list>
		</div>
		<div class="container">
			<h5>transition between multiple elements</h5>
			<!-- case in which you can have 2 elements because one is added at the time -->
			<transition name="fade-button" mode="out-in">
				<button @click="showUsers" v-if="!usersAreVisible">Show Users</button>
				<button @click="hideUsers" v-else>Hide Users</button>
			</transition>
		</div>
		<div class="container">
			<h5>animating modal</h5>
			<button @click="showDialog">Show Dialog</button>
		</div>
		<div class="container">
			<h5>transition component</h5>
			<!-- :css="false" disabled CSS -->
			<transition
				:css="false"
				@before-enter="beforeEnterExample"
				@enter="enterExample"
				@after-enter="afterEnterExample"
				@before-leave="beforeLeaveExample"
				@leave="leaveExample"
				@after-leave="afterLeaveExample"
				@enter-cancelled="enterCancelledExample"
				@leave-cancelled="leaveCancelledExample"
			>
				<!-- transition wrapper - for element's that are added to the DOM -->
				<!-- can be used for animations as well not just transitions -->
				<p v-if="paraIsVisible">This is only sometimes visible...</p>
			</transition>
			<button @click="toggleParagraph">Toggle Paragraph</button>
		</div>
		<div class="container">
			<div class="block" :class="{ animate: blockAnimated }"></div>
			<button @click="animateBlock">Animate</button>
		</div>
		<base-modal @close="hideDialog" :open="dialogIsVisible">
			<p>This is a test dialog!</p>
			<button @click="hideDialog">Close it!</button>
		</base-modal>
	</router-view>
</template>

<script>
import UsersList from './components/UsersList.vue';
export default {
	components: {
		UsersList,
	},
	data() {
		return {
			dialogIsVisible: false,
			blockAnimated: false,
			paraIsVisible: false,
			usersAreVisible: false,
			enterInterval: null,
			leaveInterval: null,
		};
	},
	methods: {
		showDialog() {
			this.dialogIsVisible = true;
		},
		hideDialog() {
			this.dialogIsVisible = false;
		},
		animateBlock() {
			this.blockAnimated = true;
		},
		toggleParagraph() {
			this.paraIsVisible = !this.paraIsVisible;
		},
		showUsers() {
			this.usersAreVisible = true;
		},
		hideUsers() {
			this.usersAreVisible = false;
		},
		beforeEnterExample(element) {
			console.log('beforeEnter');
			console.log(element);
			element.style.opacity = 0;
		},
		enterExample(element, done) {
			console.log('enter');
			console.log(element);

			let round = 1;
			this.enterInterval = setInterval(() => {
				element.style.opacity = round * 0.01;
				round++;
				if (round > 100) {
					clearInterval(this.enterInterval);
					done();
				}
			}, 20);
		},
		afterEnterExample(element) {
			console.log('afterEnter');
			console.log(element);
		},
		beforeLeaveExample(element) {
			console.log('beforeLeave');
			console.log(element);
			element.style.opacity = 1;
		},
		leaveExample(element, done) {
			console.log('leave');
			console.log(element);

			let round = 1;
			this.leaveInterval = setInterval(() => {
				element.style.opacity = 1 - round * 0.01;
				round++;
				if (round > 100) {
					clearInterval(this.leaveInterval);
					done();
				}
			}, 20);
		},
		afterLeaveExample(element) {
			console.log('afterLeave');
			console.log(element);
		},
		enterCancelledExample(element) {
			console.log(element);
			clearInterval(this.enterInterval);
		},
		leaveCancelledExample(element) {
			console.log(element);
			clearInterval(this.leaveInterval);
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

button,
a {
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
		// transition: transform 0.3s ease-out;

		&.animate {
			// transform: translateX(-150px);
			animation: slide-scale 0.3s ease-out forwards;
		}
	}
}

// VUE will add classes below to the transition component
// .para-enter-from {
// 	// opacity: 0;
// 	// transform: translateY(-30px);
// }

// .para-enter-active {
// 	// transition: all 0.3s ease-out;
// 	animation: slide-scale 0.3s ease-out;
// }

// .para-enter-to {
// 	// opacity: 1;
// 	// transform: translateY(0);
// }

// .para-leave-from {
// 	// opacity: 1;
// 	// transform: translateY(0);
// }

// .para-leave-active {
// 	animation: slide-scale 0.3s ease-out;
// }

// .para-leave-to {
// 	// opacity: 0;
// 	// transform: translateY(-30px);
// }

// button transition
.fade-button-enter-from,
.fade-button-leave-to {
	opacity: 0;
}

.fade-button-enter-active {
	transition: opacity 0.3s ease-out;
}

.fade-button-leave-active {
	transition: opacity 0.3s ease-in;
}

.fade-button-enter-to,
.fade-button-leave-from {
	opacity: 1;
}

.route-enter-active {
	animation: slide-scale 0.3s ease-out;
}
.route-leave-active {
	animation: slide-scale 0.3s ease-in;
}

@keyframes slide-scale {
	0% {
		transform: translateX(0) scale(1);
	}

	70% {
		transform: translateX(-120px) scale(1.1);
	}

	100% {
		transform: translateX(-150px) scale(1);
	}
}

h5 {
	width: 100%;
	margin: 0;
	text-align: left;
}
</style>