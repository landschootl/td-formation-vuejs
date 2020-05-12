<template>
  <div id="app">
    <Products></Products>
  </div>
</template>

<script>
import Products from './components/Products.vue'

export default {
  name: 'App',
  components: {
    Products
  }
}
</script>

<style>
  body {
    background-color: white;
    margin: 0px;
    padding: 15px;
  }
  #app {
    text-align: center;
    padding: 0px 200px;
  }
</style>
