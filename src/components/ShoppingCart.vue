<template>
  <div>
    <div v-for="item in cart" :key="item.name" class="cart-item">
      <img :src="'/img/' + item.image" :alt="item.name" class="img-thumbnail">
      <h4>{{ item.name }}</h4>
      <p>Precio: ${{ item.price }}</p>
      <p>Cantidad: {{ item.quantity }}</p>
      <button class="btn btn-danger" @click="removeFromCart(item)">Remover del carrito</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['cart'],
  methods: {
    removeFromCart(item) {
      this.$emit('remove-from-cart', item);
    }
  }
};
</script>

<style>
.cart-item {
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
