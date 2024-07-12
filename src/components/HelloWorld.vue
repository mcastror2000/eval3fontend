<template>
  <div>
    <div v-for="product in products" :key="product.name" class="product">
      <img :src="product.image" :alt="product.name" class="img-thumbnail">
      <h4>{{ product.name }}</h4>
      <p>Precio: ${{ product.price }}</p>
      <p>Stock: {{ product.stock }}</p>
      <button class="btn btn-primary" @click="addToCart(product)">Agregar al carrito</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        { name: 'Audífono', price: 30000, stock: 3, image: 'img/audifono.jpg' },
        { name: 'Mouse', price: 20000, stock: 5, image: 'img/mouse.jpg' },
        { name: 'Teclado', price: 15000, stock: 10, image: 'img/teclado.jpg' },
        { name: 'Gabinete', price: 35000, stock: 4, image: 'img/gabinete.jpg' },
        { name: 'Pantalla', price: 175000, stock: 3, image: 'img/pantalla.jpg' },
        { name: 'Silla', price: 150000, stock: 2, image: 'img/silla.jpg' }
      ]
    }
  },
  methods: {
    addToCart(product) {
      this.$emit('add-to-cart', product);
    }
  }
}
</script>

<style scoped>
.product {
  margin-bottom: 20px;
}
.img-thumbnail {
  width: 100px;
  height: 100px;
}
</style>
