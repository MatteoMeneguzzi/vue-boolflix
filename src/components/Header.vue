<template>
	<header>
		<div class="container">
			<div class="logo">
				Netflix
			</div>
			<div class="searchbar">
				<input
					type="text"
					placeholder="Search your movie"
					v-model.trim="searchText"
				/>
				<button
					type="submit"
					@click.prevent="$emit('performSearch', searchText)"
				>
					Search
				</button>
			</div>
		</div>
	</header>
</template>

<script>
export default {
	name: "Header",
	data() {
		return {
			searchText: "",
		};
	},
};
</script>

<style scoped lang="scss">
header {
	background: #222;
	.container {
		display: flex;
		justify-content: space-between;
		.logo {
			color: red;
		}
	}
}
</style>
