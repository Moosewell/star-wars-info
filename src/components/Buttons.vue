<template>
<div>
  <button :disabled="this.data.previous == null" v-on:click="$emit('SwitchPage', this.data.previous)">Previous page</button>
  <label>Page {{CalculatePage}} out of {{CalculatePageAmount}}</label>
  <button :disabled="this.data.next == null" v-on:click="$emit('SwitchPage', this.data.next)">Next page</button>
</div>
</template>

<script>

export default {
  name: 'List',
  props: {
    data: Object,
  },
  data: () => ({
    

  }),
  computed:{
    CalculatePage(){
      if(this.data.next != null)
      {
        let str = this.data.next
        return str.slice(-1) - 1
      }
      if(this.data.previous != null)
      {
        let str = this.data.previous
        return parseFloat(str.slice(-1)) + 1
      }
      return 1
    },
    CalculatePageAmount(){
      return Math.ceil(this.data.count / 10)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
