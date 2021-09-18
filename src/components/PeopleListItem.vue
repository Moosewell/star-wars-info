<template>
  <div>
      {{this.data.name}}
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
