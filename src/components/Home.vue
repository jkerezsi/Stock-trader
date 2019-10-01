<template>
  <div class="container">
    <div class="box">
      <h1>Trade or View your Portfolio</h1>
      <p>You may save or load your Data</p>
      <p>Click on End Day to begin a New Day</p>
      <div class="funds">
        <h3>Yours funds: {{funds | currency}}</h3>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainPage",
  computed: {
    funds() {
      return this.$store.getters.funds;
      console.log(this.$store.getters);
    }
  }
};
</script>

<style scoped>
</style>