<template>
  <div class="products">
    <h1 class="md-display-2">Gestion de mes produits :</h1>
    <save-product :isEditMode="isEditMode" :product="productEdit" @saveProductEvent="saveProduct()"></save-product>
    <h2 class="md-display-1">La liste de mes produits :</h2>
    <md-progress-spinner v-if="isLoadProducts" md-mode="indeterminate"></md-progress-spinner>
    <md-table v-else id="products-tab">
      <md-table-row>
        <md-table-head md-numeric>ID</md-table-head>
        <md-table-head>Name</md-table-head>
        <md-table-head>Price</md-table-head>
        <md-table-head>CreatedAt</md-table-head>
        <md-table-head>UpdatedAt</md-table-head>
        <md-table-head>Action</md-table-head>
      </md-table-row>

      <md-table-row v-for="(product, index) in products" :key="index">
        <md-table-cell md-numeric>{{product.id}}</md-table-cell>
        <md-table-cell>{{product.name}}</md-table-cell>
        <md-table-cell>{{product.price}}</md-table-cell>
        <md-table-cell>{{product.createdAt}}</md-table-cell>
        <md-table-cell>{{product.updatedAt}}</md-table-cell>
        <md-table-cell>
          <md-button @click="updateProduct(product)">Modifier</md-button>
        </md-table-cell>
      </md-table-row>
    </md-table>
    <md-button class="md-raised" @click="createProduct()">Créer un nouveau produit</md-button>
  </div>
</template>

<script>
import SaveProduct from "./SaveProduct";

export default {
  name: 'Products',
  components: {
    SaveProduct
  },
  data() {
    return {
      urlApi: 'https://node-baseapi.herokuapp.com/api',
      products: [],
      isLoadProducts: true,
      productEdit: {name: '', price: 0}
    }
  },
  methods: {
    loadProducts() {
      this.axios.get(`${this.urlApi}/products`)
        .then(result => this.products = result.data.result)
        .catch(error => console.log('Impossible de charger les produits', error))
        .finally(() => this.isLoadProducts = false);
    },
    saveProduct() {
      if (this.isEditMode) {
        this.axios.put(`${this.urlApi}/products/${this.productEdit.id}`, this.productEdit)
                .then(result => {
                  const newProduct = result.data.result;
                  this.products = this.products.map(product => product.id === newProduct.id ? newProduct : product);
                  this.updateProduct(newProduct);
                })
                .catch(error => console.log('Impossible de charger les produits', error));
      } else {
        this.axios.post(`${this.urlApi}/products`, this.productEdit)
          .then(result => {
            const newProduct = result.data.result;
            this.products.push(newProduct);
            this.updateProduct(newProduct);
          })
          .catch(error => console.log('Impossible de charger les produits', error));
      }
    },
    updateProduct(product) {
      this.productEdit = Object.assign({}, product);
    },
    createProduct() {
      this.productEdit = {name: '', price: 0};
    }
  },
  created() {
    this.loadProducts();
  },
  computed: {
    isEditMode() {
      return this.productEdit.id !== undefined;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #products-tab {
    weight: 300px;
  }
</style>
