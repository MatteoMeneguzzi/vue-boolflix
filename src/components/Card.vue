<template>
	<div class="card-content">
		<img
			v-if="info.poster_path !== null"
			:src="
				`https://image.tmdb.org/t/p/w342${info.poster_path}`
					? `https://image.tmdb.org/t/p/w342${info.poster_path}`
					: `https://www.altavod.com/assets/images/poster-placeholder.png`
			"
			:alt="info.title ? info.title : info.name"
		/>
		<img
			v-else
			src="https://www.altavod.com/assets/images/poster-placeholder.png"
			alt="placeholder-image"
		/>
		<ul>
			<li><strong>Title:</strong> {{ info.title ? info.title : info.name }}</li>
			<li>
				<strong>Original title:</strong>
				{{ info.original_title ? info.original_title : info.original_name }}
			</li>
			<li class="language">
				<div class="desc"><strong>Original language:</strong></div>
				<img
					v-if="isFlag(info.original_language)"
					:src="
						require(`@/assets/flags-boolflix/${info.original_language}.png`)
					"
					:alt="info.original_language"
				/>
				<span v-else>{{ info.original_language }}</span>
			</li>
			<li class="vote">
				<strong>Vote average: </strong>
				<i
					v-for="i in oneToFive(info.vote_average)"
					:key="`full-${i}`"
					class="fas fa-star"
				></i>
				<i
					v-for="i in 5 - oneToFive(info.vote_average)"
					:key="`empty-${i}`"
					class="far fa-star"
				></i>
			</li>
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
		};
	},
	methods: {
		isFlag(lang) {
			return this.flagsImg.includes(lang);
		},
		oneToFive(num) {
			return Math.round(num) / 2;
		},
	},
};
</script>

<style scoped lang="scss">
@import "@/scss/vars";

.card-content {
	position: relative;
	width: calc(100% / 4 - 40px);
	margin: 0px 20px;
	margin-bottom: 60px;
	z-index: 0;
	img {
		max-width: 100%;
		min-height: 100%;
	}
	ul {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 100%;
		list-style: none;
		padding: 30px 20px;
		background: rgba(34, 34, 34, 0.8);
		z-index: 1;
		opacity: 0;
		transition: opacity 0.4s;
		&:hover {
			opacity: 1;
		}
		li {
			width: 100%;
			margin-bottom: 15px;
			color: $text-color-one;
			display: inline-block;
			line-height: 22px;
			letter-spacing: 0.5px;
		}
		li.language {
			position: relative;
			img {
				position: absolute;
				top: 0;
				left: 60%;
				display: inline-block;
				width: 30px;
			}
		}
		i {
			color: $text-color-two;
		}
		i.far {
			color: $text-color-one;
		}
	}
}

li.language {
	width: 30px;
	img {
		max-width: 100%;
		height: auto;
	}
}
</style>
