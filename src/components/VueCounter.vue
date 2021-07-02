<template>
  <div class="counter">
    <p>Counter value at {{ count }}</p>
    <UserButton button-text="+1" :clicked-func="increaseValue" />
    <UserButton button-text="-1" :clicked-func="decreaseValue" />
    <UserButton button-text="Reset" :clicked-func="resetValue" />
  </div>
</template>

<script>
import UserButton from "@/components/UserButton";
export default {
  name: "VueCounter",
  components: {UserButton},
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increaseValue() {
      this.count = this.count + 1;
    },
    decreaseValue() {
      this.count = this.count - 1;
    },
    resetValue() {
      this.count = 0;
    }
  }
}
</script>

<style scoped>
  .counter {
    font-size: 3.2rem;
  }
</style>