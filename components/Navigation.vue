<template>
	<div id="nav-wrapper">
		<div id="section-one" class="nav-section">
			<nuxt-link id="name" to="/" exact>Sam Harris</nuxt-link>
		</div>
		<div id="section-two" class="nav-section">
			<nuxt-link class="page-link" to="/episodes" active-class="active">Episodes</nuxt-link>
			<nuxt-link class="page-link" to="/youtube" active-class="active">YouTube</nuxt-link>
			<div id="sort-icon-wrapper" @click="toggleSorter">
				<img id="sort-icon" src="@/static/icons/sort.svg">
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Navigation',
	data () {
		return {
			scroll_old: 0,
			scroll_new: 0
		}
	},
	methods: {
		handleScroll: function() {
			let y = window.scrollY
			this.scroll_new = y
			let nav_wrapper = document.getElementById("nav-wrapper")
			let sorter = document.getElementById("sorter")
			if (this.scroll_new > this.scroll_old) {
				nav_wrapper.classList.add("nav-hidden")
				this.scroll_old = y
				if (sorter && sorter !== null) {
					sorter.classList.add("sorter-offset")
				}
			} else if (this.scroll_new < this.scroll_old) {
				nav_wrapper.classList.remove("nav-hidden")
				this.scroll_old = y
				if (sorter && sorter !== null) {
					sorter.classList.remove("sorter-offset")
				}
			}
		},
		toggleSorter: function() {
			let sorter = document.getElementById("sorter")
			sorter.classList.toggle("hide")
		},
		toggleMenu: function () {
			let menu = document.getElementById("main-menu")
			let overlay = document.getElementById("overlay")
			menu.classList.toggle("shown")
			overlay.classList.toggle("overlay-shown")
		}
	},
	mounted() {
		window.addEventListener('scroll', this.handleScroll)
	}
}
</script>

<style lang="sass">
#nav-wrapper
	position: fixed
	top: 0
	left: 0
	width: 100%
	z-index: 3
	@include flexCenter
	justify-content: flex-end
	background: var(--theme-itemWhite)
	box-shadow: 0 0 0.5rem 0.125rem rgba(black, 0.1)
	&.nav-hidden
		top: -3rem
	.nav-section
		@include flexCenter
		&#section-one
			width: auto
			justify-content: flex-start
		&#section-two
			flex: 1
			cursor: pointer
			justify-content: flex-end
		#name, .page-link
			padding: 0.33rem
			cursor: pointer
			height: 2rem
			@include flexCenter
			text-decoration: none
			background: var(--theme-itemWhite)
			&.active
				background: var(--theme-whiteBG)
		#sort-icon-wrapper
			@include flexCenter
			#sort-icon
				padding: 0.33rem
				cursor: pointer
				height: 1.25rem
				width: 1.25rem
				box-sizing: content-box
				filter: var(--theme-icon)
</style>
