<template>
	<div id="single-blog">
		<h1>{{ blog.title }}</h1>
		<article>{{ blog.content }}</article>
		<p>Author : <strong>{{ blog.author }}</strong></p>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				id: this.$route.params.id,
				blog: {}
			}
		},
		created() {
			this.$http.get('https://vuejs-firststeps.firebaseio.com/posts/' + this.id + '.json')
				.then( (data) => {
					return data.json();
				})
				.then( (data) => {
					this.blog = data;
				})
		}
	}
</script>

<style scoped>
	#single-blog{
		max-width: 500px;
		margin: 0 auto;
	}
</style>
