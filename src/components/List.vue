<template>
  <div>
    <ul class="list" v-for="(item, index) in this.data" :key="index">
      <ListItem v-bind:data="item"/>
    </ul>
  </div>
</template>

<script>
import ListItem from './ListItem.vue'

export default {
  name: 'List',
  props: {
    data: {
      type: Object, 
      default: {results: []}
    },
  },
  components: {ListItem}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
