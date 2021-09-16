<template>
  <div>
    <button v-on:click="$emit('pickCategory', 'films')">Films</button>
    <button v-on:click="$emit('pickCategory', 'people')">People</button>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  props: {
  },
  methods: {
  },
  mounted: function(){
      this.$emit('pickCategory', 'films')
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
