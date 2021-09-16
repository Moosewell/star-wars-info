<template>
  <div>
    <SearchBar ref="search" v-on:SearchData="handleSearchData" v-bind:category="searchCategory"/>
    <Menu v-on:pickCategory="handlePickCategory"/>
    <List v-bind:data="data"/>
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
    data: null,
  }),
  methods:{
    handlePickCategory(category) {
      this.searchCategory = category
      this.$refs.search.Search()
    },
    handleSearchData(searchData){
      this.data = searchData
    }
  },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
