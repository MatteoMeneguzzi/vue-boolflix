<template>
	<header>
		<div class="container">
			<div class="logo">
				<a href="https://fontmeme.com/netflix-font/"
					><img
						src="https://fontmeme.com/permalink/210513/b778d9f1e061df22720da2fcbd1ac426.png"
						alt="netflix-font"
						border="0"
				/></a>
			</div>
			<ul class="menu-inline">
				<li v-for="section in sections" :key="section">
					<a
						href="#"
						:class="{ active: section.active }"
						@click="isActive()"
						:key="section"
						>{{ section.name }}</a
					>
				</li>
			</ul>
			<ul class="menu-inline-searchbar">
				<li>
					<input
						type="text"
						placeholder="Titles, peoples, genres"
						v-model.trim="searchText"
					/>
				</li>
				<li>
					<button
						type="submit"
						@click.prevent="$emit('performSearch', searchText)"
					>
						<i class="fas fa-search"></i>
					</button>
				</li>
				<li>
					<a href="#">BAMBINI</a>
				</li>
				<li>
					<a href=""><i class="fas fa-bell"></i></a>
				</li>
				<li>
					<a href=""><i class="far fa-smile"></i></a>
				</li>
				<li>
					<a href="#">
						<i class="fas fa-sort-down"></i>
					</a>
				</li>
			</ul>
		</div>
	</header>
</template>

<script>
export default {
	name: "Header",
	data() {
		return {
			searchText: "",
			sections: [
				{ name: "Home", active: false },
				{ name: "TV Series", active: false },
				{ name: "Movies", active: false },
				{ name: "New & Popular", active: false },
				{ name: "My List", active: false },
			],
		};
	},
	methods: {
		isActive() {
			this.section.active != this.section.active;
		},
	},
};
</script>

<style scoped lang="scss">
@import "@/scss/vars";

header {
	position: fixed;
	top: 0;
	right: 0;
	left: 0;
	height: 150px;
	z-index: 1;
	background: $background-color-two;
	.container {
		z-index: 1;
		position: relative;
		display: flex;
		height: 150px;
		justify-content: space-between;
		align-items: center;
		.logo {
			margin-left: -10px;
			margin-right: 20px;
		}
		ul.menu-inline {
			display: flex;
			list-style: none;
			align-items: center;
			flex-grow: 1;
			li {
				margin-right: 5px;
				margin-left: 5px;
				a {
					text-decoration: none;
					color: #bbb;
					transition: color 0.2s;
				}
				&:hover {
					a {
						color: #ddd;
					}
				}
				a.active {
					font-weight: bold;
					vertical-align: 2px;
				}
			}
		}
		ul.menu-inline-searchbar {
			display: flex;
			list-style: none;
			align-items: center;
			li {
				margin-left: 20px;
				input {
					outline: none;
					padding: 10px;
					border: 1px solid $text-color-one;
					background-color: $background-color-one;
					color: $text-color-one;
				}
				button {
					color: $text-color-one;
					border: none;
					background-color: $background-color-two;
					cursor: pointer;
				}
				a {
					text-decoration: none;
					color: #bbb;
					transition: color 0.2s;
				}
				&:hover {
					a {
						color: #ddd;
					}
				}
				&:active {
					a {
						font-weight: bold;
					}
				}
				i.fa-bell {
					font-size: 24px;
					position: relative;
					&::after {
						content: "2";
						text-align: center;
						line-height: 20px;
						color: $text-color-one;
						background: $text-color-two;
						border-radius: 50%;
						position: absolute;
						top: -5px;
						right: -5px;
						width: 20px;
						height: 20px;
						font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
						font-size: 14px;
					}
				}
				i.fa-smile {
					font-size: 30px;
					height: 40px;
					width: 40px;
					background-color: rgb(29, 146, 150);
					color: white;
					padding: 5px 0px 0px 5px;
				}
				i.fa-sort-down {
					margin-left: -10px;
				}
			}
		}
	}
}
</style>
