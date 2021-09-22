<template>
  <div class="menu-container">
    <button :disabled="data.isFetching" class="films" v-on:click="$emit('pickCategory', 'films')">Films</button>
    <button :disabled="data.isFetching" class="people" v-on:click="$emit('pickCategory', 'people')">People</button>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  props: {
    data: Object
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
  .menu-container{
    width: 80vw;
    display: flex;
    flex-direction: row;
    margin: auto;
  }

  button{
  width: 40vw;
  height: 8vw;
  font-size: 5vw;
  color: #020619;
  border: none;
  }
  .films{
    background-color: #7a0d0c;
    border-top-left-radius: 0.5vw;
    border: solid 0.5vw #7a0d0c;
  }
  .films:hover{
    border-top-color: #ffe81f;
    border-left-color: #ffe81f;
  }
  .people{
    background-color: #0b5689;
    border-top-right-radius: 0.5vw;
    border: solid 0.5vw #0b5689;
  }
  .people:hover{
    border-top-color: #ffe81f;
    border-right-color: #ffe81f;
  }
</style>
