<template>
	<div id="app">
		<!-- HEADER -->
		<Header @performSearch="getData" />
		<!-- CONTENT -->
		<Content :movies="movieList" :series="seriesList" :populars="popularList" />
	</div>
</template>

<script>
import axios from "axios";

import Header from "./components/Header.vue";
import Content from "./components/Content.vue";

export default {
	name: "App",
	components: {
		Header,
		Content,
	},
	data() {
		return {
			apiURL: "https://api.themoviedb.org/3/search/",
			apiPopularURL: "https://api.themoviedb.org/3/movie/popular?",
			apiKey: "9edc114e109b2de703ce8f7523e74506",
			movieList: [],
			seriesList: [],
			popularList: [],
			searchingText: "",
		};
	},
	created() {
		this.getColData();
	},
	methods: {
		getData(searchText) {
			console.log("Ciao", searchText);

			if (searchText !== "") {
				const apiParams = {
					api_key: this.apiKey,
					query: searchText,
					language: "it_IT",
				};

				// Chiamata API MOVIES
				axios
					.get(this.apiURL + "movie", {
						params: apiParams,
					})
					.then((res) => {
						this.movieList = res.data.results;
						console.log(this.movieList);
					});

				// Chiamata API SERIES
				axios
					.get(this.apiURL + "tv", {
						params: apiParams,
					})
					.then((res) => {
						this.seriesList = res.data.results;
					});
			}
		},
		getColData() {
			const apiParams = {
				api_key: this.apiKey,
				language: "it_IT",
			};
			axios
				.get(this.apiPopularURL, {
					params: apiParams,
				})
				.then((res) => {
					this.popularList = res.data.results;
				});
		},
	},
};
</script>

<style lang="scss">
@import "@/scss/vars";

* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
	font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
	scroll-behavior: smooth;
}

.container {
	max-width: 1500px;
	margin: 0 auto;
	padding: 20px;
}

/* width */
::-webkit-scrollbar {
	opacity: 0;
	width: 10px;
	background: $background-color-one;
}

::-webkit-scrollbar:hover {
	opacity: 1;
	width: 10px;
	background: $background-color-one;
}

/* Track */

::-webkit-scrollbar-track {
	box-shadow: inset 0 0 5px grey;
	border-radius: 10px;
	opacity: 0;
}

::-webkit-scrollbar-track:hover {
	box-shadow: inset 0 0 5px grey;
	border-radius: 10px;
	opacity: 1;
}

/* Handle */
::-webkit-scrollbar-thumb {
	background: $text-color-two;
	border-radius: 10px;
	opacity: 0;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
	background: $text-color-two;
	opacity: 1;
}
</style>
