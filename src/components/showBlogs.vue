<template>
	<div id="show-blogs">
		<h1>All blog articles</h1>
		<input type="text" name="" v-model="search" placeholder="search blocks" autofocus>
		<div class="single-blog" v-for="blog in filteredBlogs">
			<router-link v-bind:to="'/blog/'+blog.id"><h2>{{ blog.title | toUppercase }}</h2></router-link>
			<article>{{ blog.content | snippet }}</article>
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
			this.$http.get('https://vuejs-firststeps.firebaseio.com/posts.json')
				.then( (data) => {
					// this.blogs = data.body.slice(0, 10);
					return data.json().then();
				})
				.then( (data) => {
					var blogsArray = []
					for( let key in data) {
						data[key].id = key;
						blogsArray.push(data[key])
					}
					this.blogs = blogsArray;
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
	router-link{
		text-decoration: none;
	}
	#show-blogs{
		max-width: 500px;
		margin: 0 auto;
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
