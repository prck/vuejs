<template>
  <div>
    <form>
      <div class="col-sm-6 col-md-6 col-lg-6">
        <div class="panel panel-default">
          <div class="panel-heading">
            <h3>{{ stock.brand }}
              <small>(price : {{ stock.price }})</small>
            </h3>
          </div>
          <div class="quote panel-body">
            <div class="pull-left">
              <input :class="{danger : insufficientFunds}" type="number" id="quantity" class="form-control" placeholder="Quantity" v-model.number="quantity">
            </div>
            <div class="pull-right">
              <button class="btn btn-succes" :disabled="disableButton || insufficientFunds" @click.prevent="buyStock()">
              {{ insufficientFunds ? 'Insufficient Funds' : 'Buy' }}</button>
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    stock: {
      type: Object,
      default: () => {},
      require: true
    }
  },
  data() {
    return { quantity: 0 };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    disableButton() {
      return this.quantity <= 0 || !Number.isInteger(this.quantity);
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds;
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.$store.dispatch("buyStock", order);
      this.quantity = 0;
    }
  }
};
</script>

<style scoped>
.danger {
  border: 1px solid red;
}
</style>


