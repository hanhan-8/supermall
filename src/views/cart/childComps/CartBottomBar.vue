<template>
  <div class="bottom-bar">
    <div class="check-content">
      <CheckButton class="check-btn" :isChecked="isSelectAll" @click.native="checkClick" />
      <span>全选</span>
    </div>
    <div class="price">合计{{totalPrice}}</div>
    <div class="calculate">去结算</div>
  </div>
</template>

<script>
import CheckButton from "components/content/checkButton/CheckButton";

export default {
  name: "CartBottomBar",
  components: {
    CheckButton
  },
  computed: {
    totalPrice() {
      return (
        "¥" +
        this.$store.getters.cartList
          .filter(item => {
            return item.checked;
          })
          .reduce((preValue, item) => {
            return preValue + item.price * item.count;
          }, 0)
          .toFixed(2)
      );
    },
    isSelectAll() {
      if (this.$store.getters.cartList.length === 0) return false;
      // return !this.$store.getters.cartList.filter(item => !item.checked).length;
      return !this.$store.getters.cartList.find(item => !item.checked);
    }
  },
  methods: {
    checkClick() {
      if (this.isSelectAll) {
        this.$store.getters.cartList.forEach(item => (item.checked = false));
      } else {
        this.$store.getters.cartList.forEach(item => (item.checked = true));
      }
    }
  }
};
</script>

<style scoped>
.bottom-bar {
  position: relative;
  display: flex;
  align-items: center;

  border-top: 1px solid #ccc;
  background-color: #eee;
  height: 40px;
}
.check-content {
  display: flex;
  align-items: center;
  width: 90px;
  padding: 10px;
}
.check-btn {
  width: 20px;
  height: 20px;
  line-height: 20px;
  margin-right: 10px;
}
.price {
  flex: 1;
}
.calculate {
  width: 90px;
  height: 30px;
  background-color: var(--color-tint);
  color: #fff;
  text-align: center;
  line-height: 30px;
  border-radius: 15px;
  margin-right: 10px;
}
</style>