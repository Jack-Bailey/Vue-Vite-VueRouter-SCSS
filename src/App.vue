<template>
	<router-view @toggle-dark="toggleDark"> </router-view>
</template>

<script>

export default {
	data () {
		return {
			dark: false
		}
	},
	computed: {
		prefersDark () {
			return window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches
		},
	},
	methods: {
		toggleDark () {
			this.dark = !this.dark
		}
	},
	mounted () {
		if (localStorage.getItem("dark") != null) {
			this.dark = localStorage.getItem("dark")
		} else {
			this.dark = this.prefersDark
		}
	},
	watch: {
		dark (dark) {
			if (dark) document.documentElement.classList.add("dark")
			else  document.documentElement.classList.remove("dark")
		}
	}
}

</script>


<style lang="scss">
body {
	background: var(--bg-color-1);
}
#app {
	color: var(--color-1);
	height: 100%;
	width: 80%;
	margin: 0 auto;
	text-align: center;
	display: flex;
	flex-direction: column;
}
</style>