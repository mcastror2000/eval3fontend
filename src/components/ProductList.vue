<template>
  <div>
    <div v-for="product in products" :key="product.name" class="product">
      <img :src="'/img/' + product.image" :alt="product.name" class="img-thumbnail">
      <h4>{{ product.name }}</h4>
      <p>Precio: ${{ product.price }}</p>
      <p>Stock: {{ product.stock }}</p>
      <button class="btn btn-primary" @click="addToCart(product)" :disabled="product.stock === 0">Agregar al carrito</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['products'],
  methods: {
    addToCart(product) {
      this.$emit('add-to-cart', product);
    }
  }
};
</script>

<style>
.product {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.img-thumbnail {
  width: 100px;
  height: 100px;
}

.btn {
  margin-top: 10px;
}
</style>
