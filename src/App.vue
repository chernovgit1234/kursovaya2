<template>
  <div class="container column">
    <form class="card card-w30">
      <this-form-comp
		@addComponent="addComponent"
	  ></this-form-comp>
    </form>

    <loader-comp v-if="loadingResume"></loader-comp>
    <div class="card card-w70" v-else>
	  <div v-if="this.listComp.length">
		 <component 
			:is="comp.currentComponent" 
			v-bind="{textValue: comp.textValue}"
			v-for="comp in listComp"
			:key="comp"
		></component> 
	  </div>
	  
      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>

  <div class="container">
    <p>
      <button 
		class="btn primary"
		@click="loadComments" 
		v-if="dataComments.length === 0"
		>Загрузить комментарии
	  </button>
    </p>
    
    <loader-comp v-if="loadingComments"></loader-comp>
	<div class="card" v-else>
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" 
			v-for="item in dataComments" 
			:key="item">
	      <comments-comp :item="item"></comments-comp>
		</li>
      </ul>
    </div>
  </div>
</template>

<script>
import AvatarComp from './AvatarComp'
import TextComp from './TextComp'
import TitleComp from './TitleComp'
import SubtitleComp from './SubtitleComp'
import CommentsComp from './CommentsComp.vue'
import LoaderComp from './LoaderComp.vue'
import axios from 'axios'
import ThisFormComp from './ThisFormComp.vue'

export default {
  methods: {
     async addComponent(objectFromForm) {
		this.currentComponent = objectFromForm.areaResume + '-comp'
		const obj = {currentComponent: this.currentComponent, textValue: objectFromForm.textValue }
		this.listComp.push(obj)
        try {
		const object = JSON.stringify(obj);	
	    await axios.post('https://vue-cursovaya-default-rtdb.firebaseio.com/area.json', object )
	  } catch(e) {} 
	},
	async loadComments() {
	  this.loadingComments = true
      try {
		const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
		this.dataComments = Object.keys(data).map(key => {
			return {
				email: data[key].email,
				body: data[key].body
			}
		})
		this.loadingComments = false
	  } catch(e) {}
	},
	async loadAreaResume() {
		try {
		this.loadingResume = true
		const {data} = await axios.get('https://vue-cursovaya-default-rtdb.firebaseio.com/area.json')
		if (data === null) {
			this.loadingResume = false
		}
		this.listComp = Object.keys(data).map(key => {
			return {
			  currentComponent: data[key].currentComponent,
		      textValue: data[key].textValue,
			}
		})
		this.loadingResume = false
	  } catch(e) {}
	}
  },
  data: () => ({
	textValue: '',
	areaResume: 'title',
	currentComponent: '',
	listComp: [],
	loadingComments: false,
	loadingResume: false,
	dataComments: [],
  }),
  mounted() {
    this.loadAreaResume()
  },
  components: {
	AvatarComp,
	TextComp, 
	SubtitleComp,
	TitleComp,
    CommentsComp,
    LoaderComp,
    ThisFormComp
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
