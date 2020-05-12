<template>
  <div class="products">
    <h1>La liste de mes produits :</h1>
    <md-table>
      <md-table-row>
        <md-table-head md-numeric>ID</md-table-head>
        <md-table-head>Name</md-table-head>
        <md-table-head>Price</md-table-head>
        <md-table-head>CreatedAt</md-table-head>
        <md-table-head>UpdatedAt</md-table-head>
      </md-table-row>

      <md-table-row v-for="(product, index) in products" :key="index">
        <md-table-cell md-numeric>{{product.id}}</md-table-cell>
        <md-table-cell>{{product.name}}</md-table-cell>
        <md-table-cell>{{product.price}}</md-table-cell>
        <md-table-cell>{{product.createdAt}}</md-table-cell>
        <md-table-cell>{{product.updatedAt}}</md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>

<script>
export default {
  name: 'Products',
  data() {
    return {
      urlApi: 'https://node-baseapi.herokuapp.com/api',
      products: []
    }
  },
  methods: {
    loadProducts() {
      this.axios.get(`${this.urlApi}/products`)
        .then(result => this.products = result.data.result)
        .catch(error => console.log('Impossible de charger les produits', error));
    }
  },
  created() {
    this.loadProducts();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
