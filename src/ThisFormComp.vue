<template>
	<div>
		<div class="form-control">
			<label for="areaResume">Тип блока</label>
			<select id="areaResume" v-model="areaResume"  ref="role">
			<option value="title" name="Заголовок">Заголовок</option>
			<option value="subtitle">Подзаголовок</option>
			<option value="avatar">Аватар</option>
			<option value="text">Текст</option>
			</select>
		</div>

		<div class="form-control">
			<label for="value">Значение</label>
			<textarea id="value" v-model="textValue" rows="3"></textarea>
		</div>

		<button 
			class="btn primary" 
			:disabled="activeBtnAdd"
			@click.prevent="addComponent"
		>Добавить</button>

	</div>
</template>

<script>
	export default {
		data: () => ({
			textValue: '',
			areaResume: 'title'
		}),
		computed: {
			activeBtnAdd() {
				return this.textValue.length  < 3 ? true : false
			}
		},
		methods: {
          addComponent() {
			  let areaResultSelect = this.areaResult
			  this.$emit('addComponent', {textValue: this.textValue, areaResume: this.$refs.role.value})
			  this.areaResume = 'title'
			  this.textValue = ''
		  }
		},
		emits: {
          addComponent(obj) {
            if (obj) {
				return true
			}
			console.warn('No data')
			return false
		  }
		}
		 
	}
</script>

