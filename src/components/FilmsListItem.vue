<template>
  <div>
      <label>{{this.data.title}}</label>
  </div>
</template>

<script>
export default {
  name: 'FilmsListItem',
  props: {
    data: Object,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
