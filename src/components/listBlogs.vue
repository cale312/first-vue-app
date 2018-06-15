<template>
	<div id="show-blogs" v-theme:column="'column'">
		<h1>List Blog titles</h1>
		<input type="text" name="" v-model="search" placeholder="search blocks" autofocus>
		<div class="single-blog" v-for="blog in filteredBlogs">
			<h2 v-rainbow>{{ blog.title | toUppercase }}</h2>
		</div>
	</div>
</template>

<script>

	import searchMixen from '../mixins/searchMixin'

	export default {
		components: {

		},
		data() {

			return {
				blogs: [],
				search: ""
			}

		},
		methods: {
			
		},
		created() {
			this.$http.get('https://jsonplaceholder.typicode.com/posts')
				.then( (data) => {
					this.blogs = data.body.slice(0, 10);
				})
		},
		filters: {
			toUppercase(value){
				return value.toUpperCase()
			},
			snippet(value){
				return value.slice(0,100) + '...'
			}
		},
		directives: {
			'rainbow': {
				bind(el, binding, vnode){
					el.style.color = '#' + Math.random().toString(16).slice(2,8);
				}
			},
			'theme': {
				bind(el, binding, vnode) {
					if (binding.value == 'wide') {
						el.style.maxWidth = '1200px';
					} else if (binding.value == 'narrow') {
						el.style.maxWidth = '500px';
					}

					if (binding.arg == 'column'){
						el.style.background = '#ddd';
						el.style.padding = '20px';
					}
				}
			}
		},
		mixins: [searchMixen]
	}

</script>

<style scoped>
	body{
		font-family: Verdana
	}
	#show-blogs{
		max-width: 500px;
		margin: 0 auto;
		box-shadow: 0px 2px 2px grey;
	}
	.single-blog{
		padding: 20px;
		margin: 20px 0;
		box-sizing: border-box;
		background: #eee;
		box-shadow: 0px 2px 2px grey;
	}
	input[type=text], textarea{
		display: block;
		width: 50%;
		padding: 8px;
		border: solid 1px grey;
		border-radius: 4px;
	}
</style>
