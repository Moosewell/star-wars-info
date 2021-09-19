<template>
<div>
    <ol class="list">
      <div v-for="(item, index) in this.data.results" :key="index">
      <li v-if="category == 'films'"><FilmsListItem v-bind:data="item"/></li>
      <li v-if="category == 'people'"><PeopleListItem v-bind:data="item"/></li>
      </div>
    </ol>
    <Buttons v-bind:data="data" v-on:SwitchPage="SwitchPage"/>
</div>
</template>

<script>
import FilmsListItem from './FilmsListItem.vue'
import PeopleListItem from './PeopleListItem.vue'
import Buttons from './Buttons.vue'

export default {
  name: 'List',
  props: {
    data: {
      type: Object, 
    },
    category:{
      type: String,
      default: 'films',
    }
  },
  components: {FilmsListItem, PeopleListItem, Buttons},
  methods:{
    SwitchPage(url){
      this.$emit("SwitchPage", url)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
