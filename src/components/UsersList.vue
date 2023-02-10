<template>
	<transition-group tag="ul" name="user-list">
		<li v-for="user in users" :key="user" @click="removeUser(user)">
			{{ user }}
		</li>
	</transition-group>

	<div>
		<input type="text" ref="userNameInput" />
		<button @click="addUser">Add User</button>
	</div>
</template>

<script>
export default {
	data() {
		return {
			users: ['Nikola', 'Max', 'Julie', 'Angela', 'Michael'],
		};
	},
	methods: {
		addUser() {
			const enteredUserName = this.$refs.userNameInput.value;
			this.users.unshift(enteredUserName);
		},
		removeUser(user) {
			this.users = this.users.filter((usr) => usr !== user);
		},
	},
};
</script>

<style lang="scss" scoped>
ul {
	position: relative;
	width: 100%;
	padding: 0;
	margin: 1rem 0;
	list-style: none;

	li {
		padding: 1rem;
		margin: 5px;
		text-align: center;
		border: 1px solid #ccc;
		cursor: pointer;
	}
}

input {
	padding: 0.5rem;
	border: 1px solid #42b883;
	margin: 5px;
}

.user-list-enter-from {
	opacity: 0;
	transform: translateX(-30px);
}
.user-list-enter-active {
	transition: all 1s ease-out;
}
.user-list-enter-to,
.user-list-leave-from {
	opacity: 1;
	transform: translateX(0);
}
.user-list-leave-active {
	position: absolute;
	display: block;
	width: 100%;
	transition: all 1s ease-in;
}
.user-list-leave-to {
	opacity: 1;
	transform: translateX(30px);
}

.user-list-move {
	transition: transform 0.8s ease;
}
</style>