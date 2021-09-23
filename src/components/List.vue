<template>
<div class="list-container" v-bind:class="{ films: category == 'films' }">
  <Buttons v-bind:data="data" v-on:SwitchPage="SwitchPage" v-bind:category="category"/>
    <ol class="list" v-if="CheckData">
      <hr v-if="this.data.results != 0" v-bind:class="{filmsLine: category == 'films'}">
      <div v-for="(item, index) in this.data.results" :key="index">
      <li v-if="category == 'films'"><FilmsListItem class="listItem" v-bind:class="{filmsButtons: category == 'films'}" v-bind:data="item" v-on:ToggleFilmInfo="ToggleFilmInfo" v-bind:category="category"/></li>
      <li v-if="category == 'people'"><PeopleListItem class="listItem" v-bind:class="{filmsButtons: category == 'films'}" v-bind:data="item" v-on:TogglePeopleInfo="TogglePeopleInfo" v-bind:category="category"/></li>
      <hr v-bind:class="{filmsLine: category == 'films'}">
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
  min-height: 45vh;
}

li{
  margin-bottom: 1vw;
}

ol{
  padding-left: 8vw;
}
.listItem::v-deep ul{
  padding-left: 4vw;
  width: 60vw;
}
.listItem::v-deep li{
  margin-bottom: 1vw;
}

.films{
  border: #7a0d0c solid 0.5vw;
  background-color: #531110;
}

 .listItem::v-deep button{
  background-color: #0b5689;
  border: solid 0.1vw #152e3f;
  border-radius: 0.5vw;
  font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  margin-left: 1vw;
  width: 2.5vw;
  height: 2.5vw;
  padding: 0;
  text-align: center;
}

.listItem::v-deep button:hover{
  border: solid 0.1vw #ffe81f;
}

.filmsButtons::v-deep button{
  border: #410807 solid 0.1vw;
  background-color: #7a0d0c
}

.listItem::v-deep span{
  color: #020619;
  -webkit-text-stroke: 0.05vw #ffe81f;
}
hr{
  border: #16384e solid 0.2vw;
  background-color: #16384e;
  margin-left: -8vw;
}

.filmsLine{
  border: #4d0908 solid 0.2vw;
  background-color: #4d0908;
}


</style>
