<template>
<div>
  <Buttons v-bind:data="data" v-on:SwitchPage="SwitchPage"/>
    <ol class="list" v-if="CheckData">
      <div v-for="(item, index) in this.data.results" :key="index">
      <li v-if="category == 'films'"><FilmsListItem v-bind:data="item" v-on:ToggleFilmInfo="ToggleFilmInfo"/></li>
      <li v-if="category == 'people'"><PeopleListItem v-bind:data="item" v-on:TogglePeopleInfo="TogglePeopleInfo"/></li>
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
        return false
      }
      console.log('checkData',this.data)

      return this.data.results.length != 0
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
