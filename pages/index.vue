<template>
  <div id="wrapper">
		<div id="home-content-wrapper">
			<div id="home-title-wrapper">
				<div id="home-subtitle">An Unofficial Fan Site For</div>
				<div id="home-title">Sam Harris</div>
			</div>
			<div id="home-intro">
				<div class="home-intro-para">
					Sam Harris is the author of five New York Times best sellers. His books include The End of Faith, Letter to a Christian Nation, The Moral Landscape, Free Will, Lying, Waking Up, and Islam and the Future of Tolerance (with Maajid Nawaz). The End of Faith won the 2005 PEN Award for Nonfiction. His writing and public lectures cover a wide range of topics—neuroscience, moral philosophy, religion, meditation practice, human violence, rationality—but generally focus on how a growing understanding of ourselves and the world is changing our sense of how we should live.
				</div>
				<div class="home-intro-para">
					Sam's work has been published in more than 20 languages and has been discussed in The New York Times, Time, Scientific American, Nature, Rolling Stone, and many other publications. He has written for The New York Times, The Los Angeles Times, The Economist, The Times (London), The Boston Globe, The Atlantic, and The Annals of Neurology, among others. He also hosts the Making Sense Podcast, which was selected by Apple as one of the "iTunes Best" and has won a Webby Award for best podcast in the Science & Education category.
				</div>
				<div class="home-intro-para">
					Sam received a degree in philosophy from Stanford University and a Ph.D. in neuroscience from UCLA. He has also practiced meditation for more than 30 years and has studied with many Tibetan, Indian, Burmese, and Western meditation teachers, both in the United States and abroad. Sam has created the Waking Up App for anyone who wants to learn to meditate in a modern, scientific context.
				</div>
			</div>
			<div id="home-social-links">
				<a class="home-social-link" data-site="facebook" href="https://www.facebook.com/Samharrisorg/" target="_blank">
					<img class="home-social-link-icon" src="/icons/facebook.svg" alt="facebook">
				</a>
				<a class="home-social-link" data-site="twitter" href="https://twitter.com/SamHarrisOrg" target="_blank">
					<img class="home-social-link-icon" src="/icons/twitter.svg" alt="twitter">
				</a>
				<a class="home-social-link" data-site="youtube" href="https://www.youtube.com/user/samharrisorg/videos" target="_blank">
					<img class="home-social-link-icon" src="/icons/youtube.svg" alt="youtube">
				</a>
				<a class="home-social-link" data-site="wikipedia" href="https://en.wikipedia.org/wiki/Sam_Harris" target="_blank">
					<img class="home-social-link-icon" src="/icons/wikipedia.svg" alt="wikipedia">
				</a>
				<a class="home-social-link" data-site="website" href="https://samharris.org/" target="_blank">
					<img class="home-social-link-icon" src="/icons/link.svg" alt="website">
				</a>
			</div>
		</div>
  </div>
</template>

<script>
export default {
	
}
</script>

<style lang="sass">
#wrapper
	@include pageWrapper
	#home-content-wrapper
		@include flexCenter
		margin: 1rem auto 0 auto
		border-radius: 0.5rem
		max-width: 60rem
		box-shadow: var(--theme-boxShadow)
		background: var(--theme-whiteBG)
		padding: 0.5rem
		@media (min-width: 40rem)
			padding: 2rem
			margin: 3rem auto 0 auto
		#home-title-wrapper
			width: 100%
			@include flexCenter
			#home-title
				width: 100%
				margin: 1rem auto
				font-size: 5rem
				line-height: 5rem
				text-align: center
				letter-spacing: 0.75rem
				@include flexCenter
			#home-subtitle
				margin: 1rem auto
				font-size: 1.1rem
				@include flexCenter
		#home-intro
			margin: 2rem auto
			max-width: 50rem
			border-radius: 0.25rem
			@include flexCenter
			box-shadow: var(--theme-boxShadow)
			background: var(--theme-itemWhite)
			padding: 0.5rem
			@media (min-width: 40rem)
				padding: 1rem
			.home-intro-para
				margin: 0.75rem auto
				text-indent: 0.5rem
				font-size: 1.25rem
				line-height: 1.5rem
		#home-social-links
			@include flexCenter
			width: 100%
			max-width: 30rem
			.home-social-link
				width: auto
				flex-grow: 1
				height: 5rem
				margin: 0.25rem
				cursor: pointer
				@include flexCenter
				border-radius: 0.25rem
				&[data-site='facebook']
					background: #1877F2
				&[data-site='twitter']
					background: #1DA1F2
				&[data-site='youtube']
					background: #FF0000
				&[data-site='wikipedia']
					background: #000000
				&[data-site='website']
					background: #77DD77
				&:hover
					.home-social-link-icon
						transform: scale(1.25)
				.home-social-link-icon
					height: 3rem
					width: 3rem
					margin: 0 0.5rem
					filter: invert(1)
					box-sizing: content-box
					transition: transform 0.1s ease-in-out
</style>
