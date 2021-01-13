<template>
	<div class="avatar">
      <img :src="this.$attrs.textValue">
    </div>
</template>

<script>
	export default {
		/* props: {
			textValue: {
			  type: String,
			  required: true
			}
		} */
		//если использовать this.$attrs , то как валидировать это я не знаю, this.$attrs использую тогда только в этом компоненте
	}
</script>


