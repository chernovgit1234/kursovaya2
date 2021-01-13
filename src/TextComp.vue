<template>
  <p>{{textValue}}</p>
</template>

<script>
	export default {
		props: {
			textValue: {
			  type: String,
			  required: true,
			  validator(value) {
				return value > 3 ? true : false
			  }
			  
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>