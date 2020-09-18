<template>
	<div class="episode" :data-number="number_actual" :data-title="title_actual" :data-duration="duration" :data-date="date">
		<div class="episode-locked" v-if="this.info.locked">
			<div class="episode-locked-icon-wrapper">
				<img class="episode-locked-icon" src="/icons/lock.svg" alt="locked">
			</div>
		</div>
		<a class="episode-image-wrapper" :href="this.info.image" target="_blank">
			<img class="episode-image lazy" alt="episode" src="/img/placeholders/episode.png" :data-lazysrc="`/img/episodes/${this.info.image_local}`">
		</a>
		<div class="episode-title" v-text="this.info.title"></div>
		<div class="episode-description" v-if="has_description" v-text="this.info.description"></div>
		<div class="episode-duration" v-if="has_duration" v-text="getDuration(this.info.duration)"></div>
		<div class="episode-links" :class="{ 'disabled': this.info.locked }">
			<a class="episode-link link" :href="this.info.link" target="_blank">
				<div class="episode-icon-wrapper">
					<img class="episode-icon" src="/icons/link.svg" alt="link">
				</div>
				<div class="episode-link-text">Link</div>
			</a>
			<div class="episode-link listen" @click="play">
				<div class="episode-icon-wrapper">
					<img class="episode-icon" src="/icons/media.svg" alt="listen">
				</div>
				<div class="episode-link-text">Listen</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Episode',
	props: {
		info: {}
	},
	computed: {
		title_actual: function() {
			return this.info.has_short_title ? this.info.short_title : this.info.title
		},
		number_actual: function() {
			return this.info.number !== null ? this.info.number : null
		},
		has_duration: function() {
			return this.info.duration !== null ? true : false
		},
		duration: function() {
			return this.info.duration !== null ? Math.round(this.info.duration) : null
		},
		has_description: function() {
			return this.info.description !== "" ? true : false
		},
		date: function() {
			return this.info.date !== null ? this.info.date : null
		}
	},
	methods: {
		getDuration: function(i) {
			if (i !== null) {
				let initial = new Date(i * 1000).toISOString().substring(11, 19)
				let final = initial.substring(0, 2) == "00" ? initial.substring(3) : initial
				return `${final}`
			} else {
				return "Unknown"
			}
		},
		play: function() {
			let player_wrapper = document.getElementById("player-wrapper")
			let player = document.getElementById("player")
			player_wrapper.classList.remove("hide")
			player_wrapper.classList.remove("minimized")
			player.src = this.info.audio
		}
	}
}
</script>

<style lang="sass">
.episode
	flex: 1
	margin: 0.25rem
	min-width: 100%
	position: relative
	animation: $pageFade
	@include flexCenter
	border-radius: 0.25rem
	background: var(--theme-whiteBG)
	box-shadow: var(--theme-boxShadowLight)
	@media (min-width: 35rem)
		min-width: 40%
		max-width: 50%
	@media (min-width: 50rem)
		min-width: 30%
	@media (min-width: 65rem)
		min-width: 23%
	&:hover
		box-shadow: var(--theme-boxShadowHover)
	.episode-locked
		top: 0
		right: 0
		position: absolute
		@include flexCenter
		.episode-locked-icon-wrapper
			@include flexCenter
			.episode-locked-icon
				box-sizing: content-box
				padding: 0.25rem
				height: 1rem
				width: 1rem
	.episode-image-wrapper
		flex: 1
		min-height: 130px
		padding: 0.5rem
		align-self: flex-start
		@include flexCenter
		box-sizing: content-box
		.episode-image
			width: auto
			max-width: 100%
			height: auto
			border-radius: 0.25rem
	.episode-title, .episode-description, .episode-duration
		height: auto
		padding: 0.5rem
		min-width: 100%
		text-align: center
		@include flexCenter
	.episode-audio
		padding: 0
	.episode-links
		width: 100%
		justify-content: space-between
		align-self: flex-end
		@include flexCenter
		&.disabled
			.listen
				opacity: 0.25
				cursor: auto
		.episode-link
			flex: 1
			cursor: pointer
			text-decoration: none
			@include flexCenter
			&.link
				justify-content: flex-start
				padding-left: 0.5rem
			&.listen
				justify-content: flex-end
				padding-right: 0.5rem
			&:hover
				.episode-icon-wrapper
					.episode-icon
						transform: scale(1.25)
			.episode-link-text
				@include flexCenter
				text-align: center
			.episode-icon-wrapper
				width: auto
				@include flexCenter
				.episode-icon
					@include flexCenter
					box-sizing: content-box
					padding: 0.5rem
					height: 1.5rem
					width: 1.5rem
					transition: all 0.1s ease-in-out
</style>
