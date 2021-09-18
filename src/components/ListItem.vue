<template>
  <div>
    <li>
      {{this.data}}
    </li>
  </div>
</template>

<script>
export default {
  name: 'List',
  props: {
    data: Object,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
