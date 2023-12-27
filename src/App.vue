<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart ({{ cart.length }})</div>
  <Home :premium="premium" @add-to-cart="updateCart"/>
</template>
<script>
import Home from './components/Home.vue';
export default {
  name: "App",
  components: {Home},
  data() {
    return {
      cart: [],
      premium: true,
    }
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    }
  }
};
</script>
