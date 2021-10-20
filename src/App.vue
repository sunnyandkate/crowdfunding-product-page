<template>
  <div id="app">
    <div class="container">
      <Header />
      <productPage />
      <Footer /> 
    </div>
  </div>
</template>

<script>

import Header from './components/Header.vue'
import productPage from './components/productPage.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    productPage,
    Footer 
  }
}
</script>

<style>
#app {
  font-family: 'Commissioner', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top:0;
}
.container{
  background-color:#d3d3d345;
}
</style>
