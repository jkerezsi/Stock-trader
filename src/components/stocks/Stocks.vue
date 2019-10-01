<template>
  <div class="container">
    <div class="row">
      <stock v-for="(stock,index) in stocks" :stock="stock" :key="index"></stock>
    </div>
  </div>
</template>

<script>
import Stock from "./Stock";

export default {
  components: {
    stock: Stock
  },
  computed: {
    stocks() {
       return this.$store.getters.stocks;
    }
  }
};
</script>

<style>
</style>