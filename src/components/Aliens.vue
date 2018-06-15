<template>
	<div id="aliens">
		<button v-on:click="deleteAlien">Delete Alien</button>
		<ul>
			<li v-for="alien in aliens" v-on:click="alien.show = !alien.show">
				<h2>{{ alien.name }}</h2>
				<h3 v-show="alien.show">{{ alien.speciality }}</h3>
			</li>
		</ul>
	</div>
</template>

<script>

	export default {
		props: {
			aliens: {
				type: Array,
				required: true
			}
		},
		data() {

			return {
				
			}

		},
		methods: {
			deleteAlien: function() {
				this.aliens.pop()
			}
		}
	}

</script>

<style scoped>
	#aliens{
		width: 100%;
		max-width: 1200px;
		margin: 40px auto;
		padding: 0 20px;
		box-sizing: border-box;
	}
	ul{
		display: flex;
		flex-wrap: wrap;
		list-style-type: none;
		padding: 0;
	}
	li{
		flex-grow: 1;
		flex-basis: 300px;
		text-align: center;
		padding: 30px;
		border: 1px solid #222;
		margin: 10px;
		cursor: pointer;
	}
</style>
