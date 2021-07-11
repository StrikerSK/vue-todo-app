<template>
  <button type="button" class="custom-button" @click="onClick">{{ buttonText }}</button>
</template>

<script>
export default {
  name: "UserButton",
  props: {
    buttonText: String
  },
  methods: {
    onClick() {
      this.$emit('btn-click');
    }
  }
}
</script>

<style scoped>
.custom-button {
  background-color: bisque;
  border: 1px solid black;
  border-radius: 1.2rem;
  width: 12.5rem;
  height: 2rem;
}
</style>