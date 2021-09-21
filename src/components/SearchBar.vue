<template>
  <div>
  <input v-model="inputString" type="text" v-bind:placeholder="searchBarPlaceholder">
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
  data: {isFetching: true},
  awaitingInput: false,
  }),
  computed: {
    searchBarPlaceholder(){
      return `Search for ${this.category}`
    },
  },
  methods: {
    async BuildSearchString()
    {
      const string = `https://swapi.dev/api/${this.category}/?`
      this.Search(string)
    },
    async Search(baseUrl){
      const url = baseUrl + `search=${this.inputString}`
      this.FetchData(url)
    },
    async FetchData(url)
    {
      this.Fetching()
      console.log(url)
      try {
				// Fetch skickar ett GET request till URL
				const response = await fetch(url)
				const data = await response.json()
        console.log('Response Status: ' + response.status)
				console.log('Data from API:', data);
        this.data = data
        //this.data[isFetching] = false
        Object.assign(this.data, {isFetching: false});
        this.$emit('SearchData', this.data)
			}
			catch(error) {
        console.log('Something went wrong. Please try again later. ')
			}
    },
    Fetching(){
      this.data.isFetching = true
      this.$emit('SearchData', this.data)
    }
  },
  watch:{
    inputString: function(){
      if (!this.awaitingInput) {
          this.Fetching()
          setTimeout(() => {
            this.BuildSearchString()
            //this.fetchResults({ query: this.inputString });
            this.awaitingInput = false;
          }, 1000); // 1 sec delay
        }
        this.awaitingInput = true;
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
