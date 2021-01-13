<template>
	<div>
      <h1 >{{textValue}}</h1>
	</div>
</template>

<script>
	export default {
		props: {
			textValue: {
			  type: String,
			  required: true,
			  validator(value) {
				return value > 3 && value <  20 ? true : false
			  }
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>