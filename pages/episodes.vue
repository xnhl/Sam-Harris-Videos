<template>
  <div id="wrapper">
		<Player />
		<Sorter episodes="true" />
    <div id="episodes-wrapper">
			<Episode v-for="(episode, index) in episodes" :key="index" :info="episode" />
		</div>
  </div>
</template>

<script>
import episodes from '@/assets/data'
import Episode from '@/components/Episode'
import Sorter from '@/components/Sorter'
import Player from '@/components/Player'
export default {
  data() {
		return {
			episodes
		}
	},
	components: {Episode, Sorter, Player},
	mounted() {
		var lazyloadImages = document.querySelectorAll('.lazy');
		var imageObserver = new IntersectionObserver((entries, observer) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					var image = entry.target;
					image.src = image.dataset.lazysrc;
					image.classList.remove('lazy');
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
