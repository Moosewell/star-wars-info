<template>
  <div>
      <label>{{this.data.title}}</label>
      <button v-on:click="ToggleInfo">{{data.isOpen ? '-' : '+'}}</button>
      <ul v-show="data.isOpen">
        <li><span>Episode ID:</span> {{this.data.episode_id}}</li>
        <li><span>Release Date:</span> {{this.data.release_date}}</li>
        <li><span>Opening Crawl:</span> {{this.data.opening_crawl}}</li>
        <li><span>Characters:</span>
          <ul v-if="CompareCharactersLength">
            <div v-for="(character, index) in characters" :key="index">
              <li><PeopleListItem v-bind:data="character" v-on:TogglePeopleInfo="TogglePeopleInfo"/></li>
            </div>
          </ul>
          <label v-else>Fetching Data...</label>
        </li>
      </ul>
  </div>
</template>

<script>
import PeopleListItem from './PeopleListItem.vue'

export default {
  name: 'FilmListItem',
  props: {
    data: Object,
    category: String,
  },

  methods:{
    ToggleInfo(){
      this.$emit("ToggleFilmInfo", this.data.title)
      //this.data.isOpen = !this.data.isOpen
      this.characters = []
      if(this.data.isOpen)
      {
        this.data.characters.forEach(character => {
          this.FetchCharacter(character)
        });
      }
    },
    async FetchCharacter(url)
    {
      try {
				// Fetch skickar ett GET request till URL
				const response = await fetch(url)
				let data = await response.json()
        
        let newData = {...data, isOpen: false}
        console.log('Response Status: ' + response.status)
				console.log('Characters from API:', newData);
        this.characters.push(newData)
			}
			catch(error) {
        console.log('Something went wrong. Please try again later. ')
			}
    },
    TogglePeopleInfo(characterName){
      let character = this.characters.find(character => character.name == characterName)
      console.log(character)
      character.isOpen = !character.isOpen
    },
  },

  data: () =>({
    characters: [],
  }),
  computed:{
    CompareCharactersLength(){
      if(!this.data.characters)
      {
        return false
      }
      return this.characters.length === this.data.characters.length
    },
  },
  components: {PeopleListItem}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
