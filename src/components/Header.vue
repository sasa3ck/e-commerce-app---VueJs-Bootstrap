<template>
  <header class="sticky-top bg-light p-3 d-flex justify-content-between align-items-center">
    <div class="d-flex align-items-center">
      <img :src="require('@/assets/images/logo.png')" alt="Logo" class="logo-img" />
      <h1 class="logo">Magazinul meu</h1>
    </div>
    <div class="cart-icon" @click="toggleCart">
      <i class="fas fa-shopping-cart"></i>
      <span v-if="cartItemCount > 0" class="badge badge-pill">{{ cartItemCount }}</span>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    cartItemCount: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    toggleCart() {
      this.$emit("toggle-cart");
    },
  },
};
</script>

<style scoped>
.logo {
  font-size: 1.5rem;
  font-weight: bold;
}

.cart-icon {
  position: relative;
  cursor: pointer;
}

.cart-icon i {
  font-size: 1.5rem;
}

.badge {
  position: absolute;
  top: 3px;
  right: 20px;
  color: rgb(36, 22, 22);
}

.logo-img {
  width: 50px;
  height: auto;
  margin-right: 15px;
}
</style>
