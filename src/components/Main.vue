<template>
  <div class="main-container">
    <SearchBar ref="search" v-on:SearchData="handleSearchData" v-bind:category="searchCategory"/>
    <Menu v-on:pickCategory="handlePickCategory" v-bind:data="data"/>
    <List v-bind:data="data" v-bind:category="searchCategory" v-on:SwitchPage="SwitchPage"/>
  </div>
</template>



<script>
import List from './List.vue'
import Menu from './Menu.vue'
import SearchBar from './SearchBar.vue'

export default {
  name: 'Main',
  props: {
  },
  components: {
    List,
    Menu,
    SearchBar,
  },
  data: () => ({
    searchCategory: null,
    data: {
      type: Object, 
      default: {},
    }
  }),
  computed:{
  },
  methods:{
    handlePickCategory(category) {
      this.searchCategory = category
      this.$refs.search.Search(`https://swapi.dev/api/${this.searchCategory}/?`)
    },
    handleSearchData(searchData){
      if(!searchData)
      {
      let newResults = searchData.results.map(result => ({...result, isOpen: false}))
      searchData.results = newResults
      }
      this.data = searchData
      console.log(this.data)
    },
    SwitchPage(url){
      this.$refs.search.FetchData(url)
    }
  },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
