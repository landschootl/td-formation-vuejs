<template>
  <div class="save-product">
    <h2 class="md-display-1">{{isEditMode ? `Modification d'un produit` : `Création d'un produit`}} :</h2>
    <form>
      <md-field>
        <label>Nom de mon produit</label>
        <md-input v-model="product.name"></md-input>
      </md-field>

      <md-field>
        <label>Prix de mon produit</label>
        <md-input v-model.number="product.price" type="number"></md-input>
      </md-field>

      <md-button class="md-raised md-primary" @click="emitSaveProduct()">Enregistrer mon produit</md-button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SaveProduct',
  props: {
    isEditMode: Boolean,
    product: Object
  },
  methods: {
    emitSaveProduct() {
      this.$emit('saveProductEvent', this.product);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
