<template>
	<div>
       <h2 style="overflow-wrap: break-word">{{textValue}}</h2>
	</div>
</template>

<script>
	export default {
		props: {
			textValue: {
			  type: String,
			  required: true,
			  validator(value) {
				return value > 3 && value <  30 ? true : false
			  }
			}
		}
	}
</script>

<style lang="scss" scoped>

</style>