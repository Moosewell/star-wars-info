<template>
  <div>
      <label>{{this.data.name}}</label>
      <button v-on:click="ToggleInfo">{{data.isOpen ? '-' : '+'}}</button>
      <ul v-if="data.isOpen">
        <li>Birth Year: {{this.data.birth_year}}</li>
        <li>Eye Color: {{this.data.eye_color}}</li>
        <li>Films:
          <ul v-if="CompareFilmLength">
            <div v-for="(title, index) in titles" :key="index" >
              <li>{{title}}</li>
            </div>
          </ul>
          <label v-else>Fetching Data...</label>
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
button{
  background-color: #0b5689;
  border: solid 0.1vw #152e3f;
  border-radius: 0.5vw;
  font-family:Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
  margin-left: 1vw;
  width: 2.5vw;
  height: 2.5vw;
  text-align: center;
}

button:hover{
  border: solid 0.1vw #ffe81f;
}
</style>
