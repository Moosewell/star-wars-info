<template>
  <div class="footer-container">
    <p>on this single page application you can with ease look up inforamtion about the star wars films and their respective characters that our app gathers from the star wars database 
https://swapi.dev/</p>
    <p>this Webpage was developed by MAx melander and shervin babaei as part of a graded 
assignment for a web-developement course within our software developer program at Newton Education Gothenburg.</p>
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
.footer-container{
  background-color: #ffe81f;
  display: flex;
  flex-direction: row;
}

p{
  color: #020619;
  margin: 3vw;
  
}
</style>
