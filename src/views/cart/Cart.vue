<template>
  <div id="cart">
    <nav-bar class="cart-nav">
      <div slot="center">购物车（{{cartLength}}）</div>
    </nav-bar>
    <scroll class="content" :pull-up-load="true" :probe-type="3" ref="scroll">
      <cart-list></cart-list>
    </scroll>
    <cart-bottom-bar />
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import CartList from "./childComps/CartList";
import CartBottomBar from "./childComps/CartBottomBar";

import Scroll from "components/common/scroll/Scroll";

export default {
  name: "Cart",
  components: {
    NavBar,
    CartList,
    CartBottomBar,
    Scroll
  },
  computed: {
    cartLength() {
      // return this.$store.state.cartList.length;
      return this.$store.getters.cartLength;
    }
  },
  activated() {
    this.$refs.scroll.refresh();
  }
};
</script>

<style scoped>
#cart {
  height: 100vh;
}
.cart-nav {
  background-color: var(--color-tint);
  color: #fff;
}
.content {
  height: calc(100% - 44px - 49px - 40px);
  overflow: hidden;
}
</style>