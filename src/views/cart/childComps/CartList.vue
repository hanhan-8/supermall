<template>
  <div class="cart-list">
    <cart-list-item v-for="(item,index) in cartList" :key="index" :item-info="item" />
  </div>
</template>

<script>
import CartListItem from "./CartListItem";

export default {
  name: "CartList",
  components: {
    CartListItem
  },
  computed: {
    cartList() {
      // return this.$store.state.cartList.length;
      return this.$store.getters.cartList;
    }
  }
};
</script>

<style scoped>
</style>