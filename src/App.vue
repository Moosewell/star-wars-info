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
  font-size: 1.3vw;
}
body{
  background-color: #020619;
  margin: 0px;
  
}
.app-container{
  display: flex;
  flex-direction: column;
}
.header {
  height: 13vw;
  flex-shrink: 0;
}

.footer {
  height: 15vw;
  flex-shrink: 0;
}

.main {
  flex: 1 0 auto;
}
@font-face {
  font-family: "Star Jedi";
  src: local("Star Jedi"), url(./fonts/Starjedi.ttf) format("truetype");
  }

</style>
