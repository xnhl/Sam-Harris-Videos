<template>
	<div id="player-wrapper" class="hide">
		<div id="player-content-wrapper">
			<div id="player-minimize" @click="minimize">
				<img id="player-minimize-icon" src="/icons/caret.svg" alt="minimize">
			</div>
			<audio id="player" src="" controls></audio>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Player',
	methods: {
		minimize: function() {
			let player = document.getElementById("player-wrapper");
			player.classList.toggle("minimized")
		}
	}
}
</script>

<style lang="sass">
#player-wrapper
	position: fixed
	bottom: 0
	left: 0
	z-index: 5
	width: 100%
	@include flexCenter
	justify-content: flex-end
	// #player
	// 	margin-right: 0.25rem
	&.minimized
		bottom: -4rem
	#player-content-wrapper
		// @include flexCenter
		padding: 0.25rem
		#player-minimize
			@include flexCenter
			justify-content: flex-end
			// width: auto
			#player-minimize-icon
				@include flexCenter
				box-sizing: content-box
				width: 1.5rem
				height: 1.5rem
				cursor: pointer
				padding: 0.25rem
				border-radius: 50%
				background: var(--theme-itemWhite)
				box-shadow: var(--theme-boxShadow)
				&:hover
					box-shadow: var(--theme-boxShadowHover)
		#player
			// flex: 1
</style>
