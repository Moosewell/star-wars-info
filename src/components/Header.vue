<template>
  <div class="header-container">
    <img src="../assets/Logo/logo.png" alt="Image of Logo">
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .header-container{
    background: rgb(214,18,2);
    background: linear-gradient(90deg, rgba(214,18,2,1) 0%, rgba(2,6,25,1) 33%, rgba(2,6,25,1) 66%, rgba(48,150,251,1) 100%);
    border-bottom-left-radius: 3vw;
    border-bottom-right-radius: 3vw;
    border:#ffe81f solid 0.2vw;
  }

  img{
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 20vw;
    padding: 2vw;
  }
</style>
