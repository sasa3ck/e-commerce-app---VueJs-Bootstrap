<template>
  <div class="cart-container" v-if="isCartOpen">
    <div class="cart-overlay" @click="closeCart"></div>
    <div class="cart-panel">
      <h2>Coş</h2>
      <ul class="cart-items list-unstyled">
        <li v-for="item in cart" :key="item.id" class="cart-item">
          <img :src="item.image" :alt="item.title" class="cart-item-image" />
          <div class="cart-item-details">
            <h5>{{ item.title }}</h5>
            <p>Preţ: {{ item.price }} Lei.</p>
            <p>Producător: {{ item.manufacturer }}</p>
            <input type="number" v-model.number="item.quantity" @change="updateQuantity(item)" :min="1"
              :max="item.stock" class="form-control" />
            <button @click="removeItem(item.id)" class="btn btn-danger btn-sm">
              Şterge
            </button>
          </div>
          <p>Total: {{ item.price * item.quantity }} Lei.</p>
        </li>
      </ul>
      <div class="cart-total">
        <h4>Valoare totală: {{ totalPrice }} Lei.</h4>
        <button class="btn btn-primary" @click="checkout">Treceți la plata</button>
      </div>
      <button class="btn btn-secondary mt-3" @click="closeCart">Închide</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ShoppingCart",
  props: {
    cart: {
      type: Array,
      default: () => [],
    },
    isCartOpen: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
    },
  },
  methods: {
    updateQuantity(item) {
      if (item.quantity < 1) item.quantity = 1;
      else if (item.quantity > item.stock) item.quantity = item.stock;
      this.$emit("update-cart", this.cart);
    },
    removeItem(itemId) {
      const updatedCart = this.cart.filter((item) => item.id !== itemId);
      this.$emit("update-cart", updatedCart);
    },
    closeCart() {
      this.$emit("close-cart");
    },
    checkout() {
      alert("Plata va fi procesată mai tirziu!");
    },
  },
};
</script>

<style scoped>
.cart-container {
  position: fixed;
  top: 80px;
  right: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: flex-end;
  z-index: 1000;
}

.cart-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
}

.cart-panel {
  background: white;
  width: 400px;
  padding: 20px;
  overflow-y: auto;
  z-index: 1001;
}

.cart-items {
  max-height: 400px;
  overflow-y: auto;
}

.cart-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.cart-item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  margin-right: 10px;
}

.cart-item-details {
  flex: 1;
}

.cart-total {
  text-align: right;
}

.form-control {
  width: 30%;
  margin-bottom: 5px;
}
</style>
