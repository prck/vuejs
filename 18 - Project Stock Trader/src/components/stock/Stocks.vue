<template>
  <div>
    <ul class="list-group">
      <app-stock v-for="stock in stocks" :key="stock.id" :stock="stock" />
    </ul>
  </div>
</template>

<script>
// import { mapGetters } from "vuex";
import Stock from "./Stock.vue";
export default {
  components: {
    appStock: Stock
  },
  computed: {
    stocks() {
      return this.$store.getters.stocks;
    }
    // ...mapGetters(["stocks"])
  }
};
</script>

<style>

</style>
