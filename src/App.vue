<template>
  <div id="app">
    <AppHeader :cartItemCount="cart.length" @toggle-cart="toggleCart" />
    <ProductList @add-to-cart="addToCart" />
    <ShoppingCart
      :cart="cart"
      :isCartOpen="isCartOpen"
      @update-cart="updateCart"
      @close-cart="toggleCart"
    />
    <AppFooter />
  </div>
</template>

<script>
import AppHeader from "./components/Header.vue";
import AppFooter from "./components/Footer.vue";
import ProductList from "./components/ProductList.vue";
import ShoppingCart from "./components/Cart.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AppFooter,
    ProductList,
    ShoppingCart,
  },
  data() {
    return {
      cart: [],
      isCartOpen: false,
    };
  },
  methods: {
    toggleCart() {
      this.isCartOpen = !this.isCartOpen;
    },
    addToCart(product) {
      const existingProduct = this.cart.find((item) => item.id === product.id);
      if (existingProduct) {
        existingProduct.quantity += product.quantity;
      } else {
        this.cart.push(product);
      }
    },
    updateCart(updatedCart) {
      this.cart = updatedCart;
    },
  },
};
</script>
