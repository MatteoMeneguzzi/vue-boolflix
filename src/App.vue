<template>
	<div id="app">
		<!-- HEADER -->
		<Header @performSearch="getData" />
		<!-- CONTENT -->
		<Content :movies="movieList" :series="seriesList" />
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
			apiKey: "9edc114e109b2de703ce8f7523e74506",
			movieList: [],
			seriesList: [],
			searchingText: "",
		};
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
	},
};
</script>

<style lang="scss">
* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
	font-family: "Montserrat", sans-serif;
}

.container {
	max-width: 1500px;
	margin: 0 auto;
	padding: 20px;
}
</style>
