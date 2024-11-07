<template>
  <div class="product-list container my-5">
    <div class="row">
      <ProductCard v-for="product in products" :key="product.id" :product="product" @add-to-cart="addToCart" />
    </div>
  </div>
</template>

<script>
import ProductCard from "./ProductCard.vue";

export default {
  name: "ProductList",
  components: {
    ProductCard,
  },
  data() {
    return {
      products: [
        { id: 1, title: "Mere", price: 20, rating: 4.5, manufacturer: "Ferma", stock: 10, image: require("@/assets/images/apple.svg") },
        { id: 2, title: "Banane", price: 30, rating: 4.3, manufacturer: "Padure", stock: 20, image: require("@/assets/images/banana.svg") },
        { id: 3, title: "Rosii", price: 50, rating: 4.0, manufacturer: "Tara", stock: 15, image: require("@/assets/images/tomato.svg") },
      ],
    };
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
  },
};
</script>

<style scoped>
.product-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
