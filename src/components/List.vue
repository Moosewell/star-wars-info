<template>
    <ol class="list">
      <div v-for="(item, index) in this.data.results" :key="index">
      <li v-if="category == 'films'"><FilmsListItem v-bind:data="item"/></li>
      <li v-if="category == 'people'"><PeopleListItem v-bind:data="item"/></li>
      </div>
    </ol>
</template>

<script>
import FilmsListItem from './FilmsListItem.vue'
import PeopleListItem from './PeopleListItem.vue'

export default {
  name: 'List',
  props: {
    data: {
      type: Object, 
      default: {results: []},
    },
    category:{
      type: String,
      default: 'films',
    }
  },
  components: {FilmsListItem, PeopleListItem}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
