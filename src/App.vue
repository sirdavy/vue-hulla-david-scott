<template>
  <div class="app" ref="app-container">
    <div class="task">
      <h1>HULLABASHOES</h1>
    </div>
  <div id="app">
    <Product />
  </div>
</template>

<script>
import Product from './components/ProductGrid.vue';

export default {
  name: 'App',
  components: {
    Product,
  },
};
</script>


<style>
.app {
  max-width: 1024px;
  margin: 0 auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  color: #606569;
}

h1 {
  font-size: 100px;
  justify: center;
  color: #9652ee
}

.link {
  color: #3a7f71;
}
</style> 
