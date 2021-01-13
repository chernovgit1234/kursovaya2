<template>	
	<div>
		<p><strong>{{item.email}}</strong></p>
		<small>{{item.body}}</small>
	</div>   
</template>

<script>
	export default {
		props: {
			item: {
				type: Object,
				required: true
			}
		}
	}
</script>
