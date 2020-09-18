<template>
  <div id="wrapper">
		<Sorter youtube="true" />
    <div id="episodes-wrapper">
			<YTEpisode v-for="(episode, index) in episodes" :key="index" :info="episode" />
		</div>
  </div>
</template>

<script>
import episodes from '@/assets/youtube'
import YTEpisode from '@/components/YTEpisode'
import Sorter from '@/components/Sorter'
export default {
  data() {
		return {
			episodes
		}
	},
	components: {YTEpisode, Sorter},
	mounted() {
		var lazyloadImages = document.querySelectorAll('.lazy')
		var imageObserver = new IntersectionObserver((entries, observer) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					var image = entry.target
					image.src = image.dataset.lazysrc
					image.classList.remove('lazy')
					imageObserver.unobserve(image)
				}
			})
		});

		lazyloadImages.forEach((image) => {
			imageObserver.observe(image)
		})
	}
}
</script>

<style lang="sass">
#wrapper
	@include pageWrapper
	position: relative
	#episodes-wrapper
		@include flexCenter
		margin: 0 auto
		align-items: stretch
</style>
