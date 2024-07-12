<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <h3>Productos disponibles</h3>
        <ProductList :products="products" @add-to-cart="addToCart" />
      </div>
      <div class="col-md-6">
        <h3>Productos en el carrito</h3>
        <ShoppingCart :cart="cart" @remove-from-cart="removeFromCart" />
      </div>
    </div>
    <div class="total">
      Total a pagar: ${{ total }}
    </div>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue';
import ShoppingCart from './components/ShoppingCart.vue';

export default {
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      products: [
        { name: 'Audífono', price: 30000, stock: 3, image: 'audifono.jpg' },
        { name: 'Mouse', price: 20000, stock: 5, image: 'mouse.jpg' },
        { name: 'Teclado', price: 15000, stock: 10, image: 'teclado.jpg' },
        { name: 'Gabinete', price: 35000, stock: 4, image: 'gabinete.jpg' },
        { name: 'Pantalla', price: 175000, stock: 3, image: 'pantalla.jpg' },
        { name: 'Silla', price: 150000, stock: 2, image: 'silla.jpg' }
      ],
      cart: []
    };
  },
  computed: {
    total() {
      return this.cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
    }
  },
  methods: {
    addToCart(product) {
      const productInStock = this.products.find(p => p.name === product.name);

      if (productInStock.stock > 0) {
        const itemInCart = this.cart.find(item => item.name === product.name);
        if (itemInCart) {
          itemInCart.quantity++;
        } else {
          this.cart.push({ ...product, quantity: 1 });
        }
        productInStock.stock--;
        if (productInStock.stock === 0) {
          alert(`No hay más unidades disponibles para ${product.name}`);
        }
      } else {
        alert(`No hay más unidades disponibles para ${product.name}`);
      }
    },
    removeFromCart(product) {
      const itemIndex = this.cart.findIndex(item => item.name === product.name);
      if (itemIndex !== -1) {
        const productInStock = this.products.find(p => p.name === product.name);
        productInStock.stock += this.cart[itemIndex].quantity;
        this.cart.splice(itemIndex, 1);
      }
    }
  }
};
</script>

<style>
@import './styles.css';
</style>
