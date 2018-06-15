<template>
	<div>
		<form-helper>
			<div slot="form-header">
				<h3>Form Two - Log In</h3>
				<p>Enter your details to log-in</p>
			</div>
			<div slot="form-fields">
				<input type="text" name="" placeholder="name" required>
				<input type="password" name="" placeholder="password" required>
			</div>
			<div slot="form-controls">
				<button v-on:click="handleSubmit">Submit</button>
			</div>
		</form-helper>
	</div>
</template>

<script>
	import formHelper from './FormHelper.vue'

	export default {
		components: {
			'form-helper': formHelper
		},
		data() {

			return {

			}

		},
		methods: {

		}
	}

</script>

<style>

</style>
