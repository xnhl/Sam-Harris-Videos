<template>
	<div class="yt-episode" :class="{ 'no-description': !has_description, 'has-short-description': has_short_description }" :data-duration="this.info.length_seconds" :data-date="this.info.date" :data-rating="this.info.rating">
		<a class="yt-episode-link-icon-wrapper" :href="this.info.link" target="_blank">
			<img class="yt-episode-link-icon" src="/icons/arrow.svg" alt="link">
		</a>
		<a class="episode-image-wrapper" :href="image_link" target="_blank">
			<img class="episode-image lazy" alt="episode" src="/img/placeholders/yt.png" :data-lazysrc="`/img/youtube/${this.info.image}`">
		</a>
		<div class="episode-info-wrapper" :href="this.info.link">
			<a class="episode-title" v-text="this.info.full_title" :href="this.info.link" target="_blank"></a>
			<a class="episode-description" v-if="has_description" v-text="description_short" :href="this.info.link" target="_blank"></a>
			<!-- <div class="episode-description" v-if="has_description" v-text="this.info.description"></div> -->
			<a class="episode-details-wrapper" :href="this.info.link" target="_blank">
				<div class="episode-date" v-text="this.info.date"></div>
				<div class="episode-duration" v-text="getDuration(this.info.length_seconds)"></div>
			</a>
		</div>
		<div class="episode-rating">
			<a class="episode-rating-text" v-text="rating_short" :href="this.info.link" target="_blank"></a>
			<a class="episode-rating-bar" :href="this.info.link" target="_blank">
				<div class="episode-rating-bar-fill" :style="rating_fill"></div>
			</a>
		</div>
	</div>
</template>

<script>
export default {
	name: 'YTEpisode',
	props: {
		info: {}
	},
	computed: {
		image_link: function() {
			let slug = this.info.link.slice(32);
			return `https://i.ytimg.com/vi/${slug}/hqdefault.jpg`
		},
		has_description: function() {
			return this.info.description !== "" ? true : false
		},
		has_short_description: function() {
			return this.info.description.length !== "" && this.info.description.length < 300 ? true : false
		},
		description_short: function(){
			let desc
			let extra = this.info.description.indexOf("Want to support the Making Sense podcast?") > -1 ? this.info.description.indexOf("Want to support the Making Sense podcast?") :
			 this.info.description.indexOf("To learn more, visit https://wakingup.com/") > -1 ? this.info.description.indexOf("To learn more, visit https://wakingup.com/") :
			 this.info.description.indexOf("More from Sam Harris here:") > -1 ? this.info.description.indexOf("More from Sam Harris here:") :
			 this.info.description.indexOf("SUBSCRIBE to gain access to all") > -1 ? this.info.description.indexOf("SUBSCRIBE to gain access to all") :
			 this.info.description.indexOf("SUBSCRIBE to continue listening") > -1 ? this.info.description.indexOf("SUBSCRIBE to continue listening") :
			 this.info.description.indexOf("More information at http://www.samharris.org") > -1 ? this.info.description.indexOf("More information at http://www.samharris.org") :
			 this.info.description.indexOf("For iPhone:") > -1 ? this.info.description.indexOf("For iPhone:") :
			 this.info.description.indexOf("Subscribe to the YT channel:") > -1 ? this.info.description.indexOf("Subscribe to the YT channel:") :
			 -1
			if (extra > -1) {
				desc = this.info.description.substring(0, extra)
			} else {
				desc = this.info.description
			}
			return desc
			// return desc.length > 500 ? `${desc.slice(0, 500)}...` : desc
			// return `${this.info.description.slice(0, 170)}...`
		},
		rating_short: function(){
			return `${this.info.rating.toFixed(2)} / 5`
		},
		rating_fill: function() {
			return `width: ${this.info.rating * 20}%;`
		}
	},
	methods: {
		getDuration: function(i) {
			if (i !== null) {
				let initial = new Date(i * 1000).toISOString().substring(11, 19);
				let final = initial.substring(0, 2) == "00" ? initial.substring(3) : initial;
				return `${final}`
				// return `Duration: ${final}`
			}
		}
	}
}
</script>

<style lang="sass">
.yt-episode
	flex: 1
	margin: 0.25rem
	min-width: 100%
	position: relative
	@include flexCenter
	animation: $pageFade
	text-decoration: none
	// flex-direction: column
	border-radius: 0.25rem
	background: var(--theme-whiteBG)
	box-shadow: var(--theme-boxShadowLight)
	// @media (min-width: 68rem)
	// 	min-width: 40%
	// 	max-width: 50%
	// @media (min-width: 35rem)
	// 	min-width: 40%
	// 	max-width: 50%
	// @media (min-width: 50rem)
	// 	min-width: 30%
	// @media (min-width: 65rem)
	// 	min-width: 23%
	&:hover
		box-shadow: var(--theme-boxShadowHover)
		.yt-episode-link-icon-wrapper
			.yt-episode-link-icon
				transform: scale(1.25) rotate(180deg)
	// &.no-description
	// 	@media (min-width: 35rem)
	// 		min-width: 40%
	// 		max-width: 50%
	// 	@media (min-width: 50rem)
	// 		min-width: 30%
	// 	@media (min-width: 65rem)
	// 		min-width: 23%
	// &.has-short-description
	// 	@media (min-width: 35rem)
	// 		min-width: 40%
			// max-width: 50%
	.yt-episode-link-icon-wrapper
		top: 0
		right: 0
		position: absolute
		.yt-episode-link-icon
			width: 1rem
			height: 1rem
			opacity: 0.5
			cursor: pointer
			padding: 0.5rem
			transition: transform 0.1s ease-in-out
			box-sizing: content-box
			transform: rotate(180deg)
	.episode-image-wrapper
		padding: 0.5rem
		width: 100%
		cursor: pointer
		@include flexCenter
		box-sizing: content-box
		@media (min-width: 60rem)
			width: auto
		.episode-image
			width: auto
			max-width: 100%
			height: auto
			border-radius: 0.25rem
	.episode-info-wrapper
		width: 100%
		flex: 1
		text-decoration: none
		@include flexCenter
		@media (min-width: 60rem)
			width: auto
		.episode-title, .episode-description
			flex: 1
			padding: 0.5rem
			min-width: 100%
			text-align: center
			@include flexCenter
			text-decoration: none
		.episode-details-wrapper
			@include flexCenter
			min-width: 100%
			max-width: 30rem
			text-decoration: none
			.episode-duration, .episode-date
				flex: 1
				min-width: 40%
				padding: 0.5rem
				text-align: center
				@include flexCenter
				text-decoration: none
		.episode-description
			text-align: left
			min-width: 100%
			word-break: break-word
			// margin: 0.5rem
			padding: 0.5rem
			text-indent: 0.5rem
			// max-width: 100%
	.episode-rating
		width: 100%
		align-self: flex-end
		padding: 0.5rem
		@include flexCenter
		.episode-rating-text
			width: auto
			@include flexCenter
			margin-right: 0.5rem
			text-decoration: none
		.episode-rating-bar
			flex: 1
			height: 1rem
			overflow: hidden
			border-radius: 0.25rem
			background: desaturate(red, 66)
			.episode-rating-bar-fill
				height: 100%
				background: desaturate(green, 66)
</style>
