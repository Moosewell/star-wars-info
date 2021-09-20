<template>
  <div>
      <label>{{this.data.name}}</label>
      <button v-on:click="ToggleInfo">{{data.isOpen ? '-' : '+'}}</button>
      <ul v-show="data.isOpen">
        <li>Birth Year: {{this.data.birth_year}}</li>
        <li>Eye Color: {{this.data.eye_color}}</li>
        <li>Films:
          <ul>
            <div v-for="(title, index) in titles" :key="index">
              <li>{{title}}</li>
            </div>
          </ul>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  name: 'PeopleListItem',
  props: {
    data: Object,
  },

  methods:{
    ToggleInfo(){
      this.$emit("TogglePeopleInfo", this.data.name)
      //this.data.isOpen = !this.data.isOpen
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
  })
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
