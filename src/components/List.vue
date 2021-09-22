<template>
<div class="list-container" v-bind:class="{ films: category == 'films' }">
  <Buttons v-bind:data="data" v-on:SwitchPage="SwitchPage"/>
    <ol class="list" v-if="CheckData">
      <div v-for="(item, index) in this.data.results" :key="index">
      <li v-if="category == 'films'"><FilmsListItem v-bind:data="item" v-on:ToggleFilmInfo="ToggleFilmInfo" v-bind:category="category"/></li>
      <li v-if="category == 'people'"><PeopleListItem v-bind:data="item" v-on:TogglePeopleInfo="TogglePeopleInfo" v-bind:category="category"/></li>
      </div>
    </ol>
    <label v-else>Fetching Data...</label>
</div>
</template>

<script>
import FilmsListItem from './FilmsListItem.vue'
import PeopleListItem from './PeopleListItem.vue'
import Buttons from './Buttons.vue'

export default {
  name: 'List',
  props: {
    data: {
      type: Object, 
    },
    category:{
      type: String,
      default: 'films',
    },
    people: []
  },
  components: {FilmsListItem, PeopleListItem, Buttons},
  methods:{
    SwitchPage(url){
      this.$emit("SwitchPage", url)
    },
    TogglePeopleInfo(characterName){
      let character = this.data.results.find(result => result.name == characterName)
      console.log(character)
      character.isOpen = !character.isOpen
    },
    ToggleFilmInfo(filmTitle){
      let film = this.data.results.find(result => result.title == filmTitle)
      console.log(film)
      film.isOpen = !film.isOpen
    },
  },
  computed:{
    CheckData(){
      if(this.data.results == null || this.data.results == undefined)
      {
        return true
      }
      console.log('checkData',this.data)

      return !this.data.isFetching
      //return this.data.results.length != 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list-container{
  border: #0b5689 solid 0.5vw;
  width: 79vw;
  margin:auto;
  margin-bottom: 5vw;
  background-color: #123e5c;
}

li{
  margin-bottom: 1vw;
}

.films{
  border: #7a0d0c solid 0.5vw;
  background-color: #531110
}



</style>
