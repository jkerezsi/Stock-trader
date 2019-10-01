<template>
  <div class="myPanel col-sm-6 col-md-4 border">
    <div class="panel panel-primary">
      <div class="panel-heading">
        <label class="panel-heading" for="stockName">{{stock.name}}</label>
        <small id="stockPrice" class="form-text">Price: {{stock.price}}</small>
      </div>
      <div class="panel-body">
        <div class="pull-left">
          <input 
          type="number" 
          placeholder="Quantity" 
          class="form-control" 
          v-model="quantity"
          :class="{danger: insufficientFunds}" />
        </div>
        <div class="pull-right">
          <button class="btn btn-success" @click="buyStock" :disabled="this.insufficientFunds || quantity<=0 || Number.isInteger(quantity)">
            {{ insufficientFunds ? 'Cannot afford' : 'BUY'}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  computed: {
    funds(){
      return this.$store.getters.funds
    },
    insufficientFunds(){
      return this.stock.price * this.quantity > this.funds
    }
  },
  methods: {
    buyStock(){
      let order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      }
      console.log(order)
      this.$store.dispatch('buyStock', order)
      this.quantity = 0;
    }
  },
  data () {
    return {
      quantity: 0,
    }
  }
};
</script>

<style scoped>
.myPanel {
  padding: 20px;
}
.danger{
  border: 1px solid red;
}
</style>