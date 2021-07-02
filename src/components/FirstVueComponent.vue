<template>
  <div>
    <h1>Hello from first component</h1>
    <p>This is my first paragraph in Vue</p>
    <p>{{ customText }}</p>
  </div>
</template>

<script>
export default {
  name: "FirstVueComponent",
  props: {
    customText: String
  }
}
</script>

<style scoped>
h1 {
  font-size: 8rem;
}

p {
  font-size: 3.2rem;
}
</style>