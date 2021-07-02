<template>
  <div>
    <form>
      <div>
        <label for="taskName">Task name</label>
        <input id="taskName" name="taskName" type="text" v-model="task.name" />
      </div>
      <div>
        <label for="description">Task description</label>
        <input id="description" name="description" type="text" v-model="task.description" />
      </div>
      <button type="submit" v-on:click="printValue">Create task</button>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

export default {
  name: "UserTask",
  data() {
    return {
      task: {
        id: "",
        name: "",
        description: ""
      }
    }
  },
  methods: {
    printValue(e) {
      e.preventDefault();

      if (!this.task.name) {
        alert("Task name not defined!")
      }

      this.task.id = uuidv4();
      console.log(this.task);
    }
  }
}
</script>

<style scoped>

</style>