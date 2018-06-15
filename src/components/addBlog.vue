<template>
	<div id="add-blog">
		<h2>Add a new Blog post</h2>
		<form v-if="!submitted">
			<label>Blog Title</label>
			<input type="text" name="" v-model.lazy="blog.title" required="" autofocus="">
			<label>Blog Content</label>
			<textarea required="" v-model.lazy="blog.content"></textarea>
			<label><strong>Author</strong></label>
			<select v-model="blog.author">
				<option v-for="author in authors">{{ author }}</option>
			</select>
			<input type="submit" value="Add Blog" v-on:click.prevent="post">
		</form>
		<div v-if="submitted">
			<h3>post has been sent</h3>
		</div>
		<div id="preview">
			<h3>Preview Blog</h3>
			<p>Blog Title: <strong>{{ blog.title }}</strong></p>
			<p>Blog Content:</p>
			<p><strong>{{ blog.content }}</strong></p>
			<p>Blog Author: <strong>{{ blog.author }}</strong></p>
		</div>
	</div>
</template>

<script>

	export default {
		components: {

		},
		data() {

			return {
				blog: {
					title: "",
					content: "",
					author: ""
				},
				authors: ['Xennon', 'Kai', 'Junnos', 'Cale'],
				submitted: false
			}

		},
		methods: {
			post: function() {
				this.$http.post('https://vuejs-firststeps.firebaseio.com/posts.json', this.blog)
				.then( (data) => {
					console.log(data);
					this.submitted = true;
				})
			}
		}
	}

</script>

<style scoped>
	body{
		font-family: verdana
	}
	input[type=submit], select{
		cursor: pointer;
	}
	input[type=submit]{
		cursor: pointer;
		padding: 10px 25px;
		border-radius: 4px;
		font-weight: bolder;
		background: #eee;
		box-shadow: 0px 2px 2px gray;
	}
	#add-blog *{
		box-sizing: border-box;
		list-style: none;
	}
	#add-blog{
		margin: 20px auto;
		max-width: 500px;
		padding: 20px;
		background: #ddd;
	}
	label{
		display: block;
		margin: 20px 0 10px;
	}
	input[type=text], textarea{
		display: block;
		width: 100%;
		padding: 8px;
		border: solid 1px grey;
		border-radius: 4px;
	}
	textarea{
		height: 200px;
		resize: none;
		overflow: auto;
		overflow-x: none;
	}
	input[type=text]:focus, textarea:focus{
		outline: none;
	}
	#preview{
		padding: 10px 20px;
		border: 1px solid #eee;
		margin: 30px 0;
		border-radius: 4px;
	}
	h3{
		margin-top: 10px;
	}
	#checkboxes input{
		display: inline-block;
		margin-right: 10px;
	}
	#checkboxes label{
		display: inline-block;
	}
</style>
