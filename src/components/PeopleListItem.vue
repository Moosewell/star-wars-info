<template>
  <div>
      <label>{{this.data.name}}</label>
      <button v-on:click="ToggleInfo">{{data.isOpen ? '-' : '+'}}</button>
      <ul v-if="data.isOpen">
        <li><span>Birth Year:</span> {{this.data.birth_year}}</li>
        <li><span>Eye Color:</span> {{this.data.eye_color}}</li>
        <li><span>Films:</span>
          <ul v-if="CompareFilmLength">
            <div v-for="(title, index) in titles" :key="index" >
              <li>{{title}}</li>
            </div>
          </ul>
          <label v-else class="fetching">Fetching Data... <img class="gif" src="../assets/gif/giphy.gif"></label>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'PeopleListItem',
  props: {
    data: Object,
    category: String,
  },

  methods:{
    ToggleInfo(){
      this.$emit("TogglePeopleInfo", this.data.name)
      this.titles = []
      if(this.data.isOpen)
      {
        this.data.films.forEach(film => {
          this.FetchTitle(film)
        });
      }
    },
    async FetchTitle(url)
    {
      try {
				// Fetch skickar ett GET request till URL
				const response = await fetch(url)
				const data = await response.json()
        console.log('Response Status: ' + response.status)
				console.log('Titles from API:', data);
        this.titles.push(data.title)
			}
			catch(error) {
        console.log('Something went wrong. Please try again later. ')
			}
    },
  },

  data: () =>({
    titles: [],
  }),
  computed:{
    CompareFilmLength(){
      if(!this.data.films)
      {
        return false
      }
      return this.titles.length === this.data.films.length
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
