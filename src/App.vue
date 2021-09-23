<template>
<div class="app-container">
  <Header class="header"/>
  <Main class="main"/>
  <Footer class="footer"/>
</div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer
  }
}
</script>
<style>
*{
  color: #ffe81f;
  font-family: "Star Jedi";
  text-transform: lowercase;
  font-size: 1.5vw;
}
body{
  background-color: #020619;
  margin: 0px;
  
}
.app-container{
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.header {
  height: 13vw;
}

.main {
  flex-grow: 1;
}
@font-face {
  font-family: "Star Jedi";
  src: local("Star Jedi"), url(./fonts/Starjedi.ttf) format("truetype");
  }

</style>
