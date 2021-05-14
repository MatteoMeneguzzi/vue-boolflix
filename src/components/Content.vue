<template>
	<section class="content">
		<div class="container">
			<h2>New & Popular</h2>
			<div class="populars" id="populars">
				<Card v-for="popular in populars" :key="popular.id" :info="popular" />
			</div>
			<h2>Movies</h2>
			<div v-show="movies.length" class="movies" id="movies">
				<Card v-for="movie in movies" :key="movie.id" :info="movie" />
			</div>
			<h2>Series</h2>
			<div class="series" id="series">
				<Card v-for="serie in series" :key="serie.id" :info="serie" />
			</div>
		</div>
		<!-- <div v-else class="loader">Loading...</div> -->
	</section>
</template>

<script>
import Card from "../components/Card";

export default {
	name: "Content",
	components: { Card },
	props: ["movies", "series", "populars"],
};
</script>

<style scoped lang="scss">
@import "@/scss/vars";

.content {
	z-index: -1;
	background: $background-color-one;
	.container {
		padding-top: 200px;
		display: flex;
		flex-direction: column;
		z-index: -1;
		h2 {
			margin-bottom: 50px;
			color: $text-color-one;
		}
		.movies,
		.series,
		.populars {
			display: flex;
			flex-wrap: wrap;
		}
	}
}
</style>
