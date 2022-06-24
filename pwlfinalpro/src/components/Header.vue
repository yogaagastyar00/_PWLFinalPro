<template>
<nav class="navbar bg-light">
    <div class="container-fluid">
        <strong><span class="navbar-brand mb-0 h1">Yo Market</span></strong>
        <span class="navbar-brand mb-0 h1">Chart ({{ totalQty }})</span>
    </div>
</nav>
</template>

<script>
import { mapGetters } from 'vuex';
export default {
  name:"Header",
  computed: {
    ...mapGetters(["cart"]),
    totalQty() {
      return this.cart.reduce((a, b) => a + b.qty, 0);   //menjumlahkan item pada cart
    },
  },
};


</script>

<style scoped>
nav {
  margin-bottom: 10px;
}
</style>
