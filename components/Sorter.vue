<template>
	<div id="sorter" class="hide">
		<div id="sorter-sort">
			<div id="sorter-text">Sort By:</div>
			<div id="sorter-items" v-if="this.youtube">
				<div class="sorter-item" @click="sortByTitle">Title</div>
				<div class="sorter-item" @click="sortByDate">Date</div>
				<div class="sorter-item" @click="sortByRating">Rating</div>
				<div class="sorter-item" @click="sortByDuration">Duration</div>
			</div>
			<div id="sorter-items" v-if="this.episodes">
				<div class="sorter-item" @click="sortByNumber">Number</div>
				<div class="sorter-item" @click="sortByTitle">Title</div>
				<div class="sorter-item" @click="sortByDuration">Duration</div>
			</div>
		</div>
		<div id="sorter-search">
			<input id="sorter-search-input" v-if="this.youtube" @input="search" @change="search" type="text" placeholder="Search">
			<input id="sorter-search-input" v-if="this.episodes" @input="search" @change="search" type="text" placeholder="Search">
		</div>
	</div>
</template>

<script>
export default {
	name: 'Sorter',
	props: {
		episodes: false,
		youtube: false
	},
	data() {
		return {
			sortTitle: 1,
			sortDate: 0,
			sortRating: 0,
			sortDuration: 0,
			sortNumber: 1
		}
	},
	methods: {
		sortByTitle: function() {
			let wrapper = document.getElementById("episodes-wrapper");
			let items = [...wrapper.children];
			let sorted
			if (this.youtube) {
				sorted = items.sort((a, b) => {
					let aa = a.getElementsByClassName("episode-title")[0].textContent.replace(/[^a-z0-9]/gi, "").toLowerCase();
					let bb = b.getElementsByClassName("episode-title")[0].textContent.replace(/[^a-z0-9]/gi, "").toLowerCase();
					return aa < bb ? -1 : aa > bb ? 1 : 0
				})
			} else if (this.episodes) {
				sorted = items.sort((a, b) => {
					let aa = a.dataset.title.replace(/[^a-z0-9]/gi, "").toLowerCase();
					let bb = b.dataset.title.replace(/[^a-z0-9]/gi, "").toLowerCase();
					return aa < bb ? -1 : aa > bb ? 1 : 0
				})
			}
			if (this.sortTitle % 2 === 0) {
				sorted = sorted.reverse()
			}
			for (let each of sorted) {
				wrapper.appendChild(each)
			}
			this.sortTitle++
			window.scrollTo(0, 0)
		},
		sortByDate: function() {
			let wrapper = document.getElementById("episodes-wrapper");
			let items = [...wrapper.children];
			let sorted = items.sort((a, b) => {
				let aa = new Date(a.dataset.date);
				let bb = new Date(b.dataset.date);
				return aa < bb ? -1 : aa > bb ? 1 : 0
			});
			if (this.sortDate % 2 === 0) {
				sorted = sorted.reverse()
			}
			for (let each of sorted) {
				wrapper.appendChild(each)
			}
			this.sortDate++
			window.scrollTo(0, 0)
		},
		sortByRating: function() {
			let wrapper = document.getElementById("episodes-wrapper");
			let items = [...wrapper.children];
			let sorted = items.sort((a, b) => {
				let aa = parseFloat(a.dataset.rating);
				let bb = parseFloat(b.dataset.rating);
				return aa < bb ? -1 : aa > bb ? 1 : 0
			});
			if (this.sortRating % 2 === 0) {
				sorted = sorted.reverse()
			}
			for (let each of sorted) {
				wrapper.appendChild(each)
			}
			this.sortRating++
			window.scrollTo(0, 0)
		},
		sortByDuration: function() {
			let wrapper = document.getElementById("episodes-wrapper");
			let items = [...wrapper.children];
			let has_duration = items.filter(item => { return (item.dataset.duration && item.dataset.duration !== null) });
			let no_duration = items.filter(item => { return (!item.dataset.duration || item.dataset.duration == null) });
			let sorted = has_duration.sort((a, b) => {
				let aa = parseInt(a.dataset.duration);
				let bb = parseInt(b.dataset.duration);
				if (this.sortDuration % 2 === 0) {
					return aa > bb ? -1 : aa < bb ? 1 : 0
				} else {
					return aa < bb ? -1 : aa > bb ? 1 : 0
				}
			});
			let final_set = sorted.concat(no_duration);
			for (let each of final_set) {
				wrapper.appendChild(each)
			}
			this.sortDuration++
			window.scrollTo(0, 0)
		},
		sortByNumber: function() {
			let wrapper = document.getElementById("episodes-wrapper");
			let items = [...wrapper.children];
			let has_number = items.filter(item => { return (item.dataset.number && item.dataset.number !== null) })
			let no_number = items.filter(item => { return (!item.dataset.number || item.dataset.number == null) })
			let sorted = has_number.sort((a, b) => {
				let aa = parseInt(a.dataset.number);
				let bb = parseInt(b.dataset.number);
				if (this.sortNumber % 2 === 0) {
					return aa > bb ? -1 : aa < bb ? 1 : 0
				} else {
					return aa < bb ? -1 : aa > bb ? 1 : 0
				}
			});
			let final_set = sorted.concat(no_number);
			for (let each of final_set) {
				wrapper.appendChild(each)
			}
			this.sortNumber++
			window.scrollTo(0, 0)
		},
		search: function() {
			setTimeout(() => {
				let wrapper = document.getElementById("episodes-wrapper");
				let items = [...wrapper.children];
				let text = document.getElementById("sorter-search-input").value.toLowerCase();
				for (let each of items) {
					let title = each.querySelector(".episode-title") !== null ? each.querySelector(".episode-title").textContent.toLowerCase().indexOf(text) : null;
					let description = each.querySelector(".episode-description") !== null ? each.querySelector(".episode-description").textContent.toLowerCase().indexOf(text) : null;
					let date = each.querySelector(".episode-date") !== null ? each.querySelector(".episode-date").textContent.toLowerCase().indexOf(text) : null;
					if (
						(title == null || title == -1)
						&& (description == null || description == -1)
						&& (date == null || date == -1)
					) {
						each.classList.add("hide")
					} else if (
						(title !== null && title > -1)
						|| (description !== null && description > -1)
						|| (date !== null && date > -1)
					) {
						each.classList.remove("hide")
					}
				}
				window.scrollTo(0, 0)
			}, 500);
		}
	}
}
</script>

<style lang="sass">
#sorter
	// position: fixed
	position: sticky
	width: 100%
	margin: 0 auto
	top: 2rem
	left: 0
	z-index: 2
	max-width: 40rem
	animation: $pageFade
	@include flexCenter
	border-radius: 0.25rem
	transition: top 0.1s ease-in-out
	background: var(--theme-itemWhite)
	box-shadow: 0 0 0.5rem 0.125rem rgba(black, 0.1)
	&.sorter-offset
		top: 0
	#sorter-sort
		@include flexCenter
		margin: auto 0.25rem
		#sorter-text
			width: auto
		#sorter-items
			flex: 1
			@include flexCenter
			.sorter-item
				text-align: center
				padding: 0.25rem
				margin: 0.25rem
				border-radius: 0.25rem
				@include flexCenter
				background: var(--theme-whiteBG)
	#sorter-search
		@include flexCenter
		padding: 0.25rem
		margin: auto 0.25rem
		#sorter-search-input
</style>
