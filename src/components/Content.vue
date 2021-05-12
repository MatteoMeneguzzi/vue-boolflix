<template>
	<section class="content">
		<div class="container">
			<h2>Movies</h2>
			<div v-show="movies.length" class="movies">
				<Card v-for="movie in movies" :key="movie.id" :info="movie" />
			</div>
			<h2>Series</h2>
			<div class="series">
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
	props: ["movies", "series"],
};
</script>

<style scoped lang="scss">
.content {
	background: #aaa;
	.container {
		display: flex;
		flex-direction: column;
		.movies,
		.series {
			display: flex;
			flex-wrap: wrap;
			h2 {
			}
		}
	}
}
</style>
