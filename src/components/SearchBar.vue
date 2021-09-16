<template>
  <div>
  <input v-model="inputString"  @keyup="Search" type="text" v-bind:placeholder="searchBarPlaceholder">
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  props: {
  category: String,
  },
  data: () =>({
  inputString: '',
  }),
  computed: {
    searchBarPlaceholder(){
      return `Search for ${this.category}`
    },
    determineUrl(){
      if(this.category == null)
      {
        return `https://swapi.dev/api/films`
      }
      if(this.inputString == '')
      {
        console.log("filterless")
        return `https://swapi.dev/api/${this.category}`
      }
      else
      {
        return `https://swapi.dev/api/${this.category}/?search=${this.inputString}`
      }
    },
  },
  methods: {
    async Search(){
      const url = this.determineUrl
      console.log(url)
      try {
				// Fetch skickar ett GET request till URL
				const response = await fetch(url)
				const data = await response.json()
        console.log('Response Status: ' + response.status)
				console.log('Data from API:', data);
        this.$emit('SearchData', data)
			}
			catch(error) {
        console.log('Something went wrong. Please try again later. ')
			}
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
