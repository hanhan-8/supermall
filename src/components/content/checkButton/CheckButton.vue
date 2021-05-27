<template>
  <div class="check-btn" :class="{check:isChecked}">
    <img src="~/assets/img/cart/tick.svg" alt />
  </div>
</template>

<script>
import CheckButton from "components/content/checkButton/CheckButton";

export default {
  name: "CheckButton",
  props: {
    isChecked: {
      type: Boolean,
      default: false
    }
  }
  // data() {
  //   return {
  //     isChecked: false
  //   };
  // },
  // methods: {
  //   btnClick() {
  //     return (this.isChecked = !this.isChecked);
  //   }
  // }
};
</script>

<style scoped>
.check-btn {
  border-radius: 50%;
  border: 2px solid #ccc;
}
.check {
  background-color: var(--color-tint);
  border-color: var(--color-tint);
}
</style>