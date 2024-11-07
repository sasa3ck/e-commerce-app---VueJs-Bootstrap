<template>
  <div class="product-card col-md-4 mb-4">
    <div class="card h-100">
      <img :src="product.image" class="card-img-top" :alt="product.title" />
      <div class="card-body">
        <h5 class="card-title">{{ product.title }}</h5>
        <p class="card-text">Preţ: {{ product.price }} Lei</p>
        <p class="card-text">Producător: {{ product.manufacturer }}</p>
        <p class="card-text">Rating: {{ product.rating }} ⭐</p>
        <p class="card-text">În stoc: {{ product.stock }} buc.</p>
        <div class="d-flex justify-content-between align-items-center">
          <input type="number" v-model.number="quantity" min="1" :max="product.stock" class="form-control w-25" />
          <button @click="addToCart" class="btn btn-primary" :disabled="quantity < 1 || quantity > product.stock">
            Adaugă in coş
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    product: Object,
  },
  data() {
    return {
      quantity: 1,
    };
  },
  methods: {
    addToCart() {
      const item = {
        ...this.product,
        quantity: this.quantity,
      };
      this.$emit("add-to-cart", item);
      this.quantity = 1;
    },
  },
};
</script>

<style scoped>
.product-card .card {
  height: 100%;
}
</style>
