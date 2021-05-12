<template>
	<div class="card-content">
		<img
			:src="
				`https://image.tmdb.org/t/p/w342${
					info.poster_path ? info.poster_path : info.backdrop_path
				}`
			"
			:alt="info.title ? info.title : info.name"
			@mouseover="hover = true"
			@mouseleave="hover = false"
		/>
		<ul>
			<li>{{ info.title ? info.title : info.name }}</li>
			<li>
				{{ info.original_title ? info.original_title : info.original_name }}
			</li>
			<li class="language">
				<img
					v-if="isFlag(info.original_language)"
					:src="
						require(`@/assets/flags-boolflix/${info.original_language}.png`)
					"
					:alt="info.original_language"
				/>
				<span v-else>{{ info.original_language }}</span>
			</li>
			<li>{{ OneToFive(info.vote_average) }}</li>
			<i class="fas fa-star"></i>
		</ul>
	</div>
</template>

<script>
export default {
	name: "Card",
	props: ["info"],
	data() {
		return {
			flagsImg: ["it", "en"],
			hover: false,
		};
	},
	methods: {
		isFlag(lang) {
			return this.flagsImg.includes(lang);
		},
		OneToFive(num) {
			return Math.round(num) / 2;
		},
	},
};
</script>

<style scoped lang="scss">
.card-content {
	position: relative;
	width: calc(100% / 4 - 40px);
	margin: 0px 20px;
	margin-bottom: 60px;
	img {
		max-width: 100%;
	}
	ul {
		position: absolute;
		top: 0;
		list-style: none;

		i {
			width: 30px;
			height: 30px;
			font-size: 20px;
			display: block;
			color: black;
			background-color: white;
		}
	}
}

li.language {
	width: 30px;
	img {
		max-width: 100%;
	}
}
</style>
