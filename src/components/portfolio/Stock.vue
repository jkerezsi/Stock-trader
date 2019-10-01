<template>
  <div class="myPanel col-sm-6 col-md-4 border">
    <div class="panel panel-info">
      <div class="panel-heading">
        <label class="panel-heading" for="stockName">{{stock.name}}</label>
        <small id="stockPrice" class="form-text">Price: {{stock.price}} || Quantity: {{stock.quantity}}</small>
      </div>
      <div class="panel-body">
        <div class="pull-left">
          <input 
          type="number" 
          placeholder="Quantity" 
          class="form-control" 
          v-model="quantity"
          :class="{danger: insufficientQuantity}" />
        </div>
        <div class="pull-right">
          <button 
          class="btn btn-success" 
          @click="sellStock" 
          :disabled=" insufficientQuantity || quantity<=0 || Number.isInteger(quantity)">
          {{ insufficientQuantity ? 'Not enough quantity' : 'SELL'}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapActions} from 'vuex';

export default {
 props: ['stock'],
   data () {
    return {
      quantity: 0,
    }
  },
  computed: {
    insufficientQuantity(){
      return this.quantity > this.stock.quantity
    }
  },
  methods: {
    ...mapActions({
      sellOrder: 'sellStock'
  }),
    sellStock() {
      console.log(this.stock)
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.sellOrder(order);
      this.quantity = 0;
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