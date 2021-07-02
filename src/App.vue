<template>
  <div id="app">
    <VueCounter />
    <UserTask />
  </div>
</template>

<script>
import VueCounter from "@/components/VueCounter";
import UserTask from "@/components/UserTask";

export default {
  name: 'App',
  components: {
    UserTask,
    VueCounter
  },
  data() {
    return {
      count: 0,
      tasks: []
    }
  },
  methods: {
    increaseValue() {
      this.count = this.count + 1;
    },
    addTask(task) {
      this.tasks.concat(task);
    }
  }
}
</script>

<style>
html {
  font-size: 62.5%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
