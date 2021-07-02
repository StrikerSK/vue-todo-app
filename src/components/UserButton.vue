<template>
  <button v-on:click="clickedFunc()">{{ buttonText }}</button>
</template>

<script>
export default {
  name: "UserButton",
  props: {
    buttonText: String,
    clickedFunc: Function
  }
}
</script>

<style scoped>
button {
  width: 8rem;
}
</style>