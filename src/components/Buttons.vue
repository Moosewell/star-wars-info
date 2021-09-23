<template>
<div class="buttons-container">
  <button :disabled="this.data.previous == null || this.data.isFetching" v-on:click="$emit('SwitchPage', this.data.previous)" v-bind:class="{films: category == 'films'}">Previous page</button>
  <label>Page {{CalculatePage}} out of {{CalculatePageAmount}}</label>
  <button :disabled="this.data.next == null || this.data.isFetching" v-on:click="$emit('SwitchPage', this.data.next)" v-bind:class="{films: category == 'films'}">Next page</button>
</div>
</template>

<script>

export default {
  name: 'List',
  props: {
    data: Object,
    category: String,
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
      let pageAmount = Math.ceil(this.data.count / 10)
      if(pageAmount > 0)
      {
        return pageAmount
      }
      return 1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.buttons-container{
  display: flex;
  flex-direction: row;
  width: 70.5vw;
  height: 5vw;
  margin: auto;
}

button{
  background-color: #0b5689;
  border-radius: 0.5vw;
  color: #020619;
  border: solid 0.1vw #152e3f;
  margin: 1vw;
  width: 25vw;
}
button:hover{
  border: solid 0.1vw #ffe81f;
}
label{
  color: #020619;
  -webkit-text-stroke: 0.05vw #ffe81f;
  margin-top: 1vw;
  margin-bottom: 1vw;
  text-align: center;
  width: 20vw;
  font-size: 1.5vw;
}

.films{
  border: #410807 solid 0.1vw;
  background-color: #7a0d0c
}

button:disabled{
  background-color: #123e5c;
}

button:disabled:hover{
border: solid 0.1vw #152e3f;
}

.films:disabled{
  background-color: #531110;
}
.films:disabled:hover{
  border: #410807 solid 0.1vw;
}
</style>
