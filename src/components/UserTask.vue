<template>
  <div class="task-box">
    <span>Task name: {{ task.name }}</span>
    <span>Task description: {{ task.description }}</span>
    <span>Task created at: {{ parseDate() }}</span>
    <span>{{ `This task is ${task.done ? "" : "not"} done` }}</span>
    <button @click="toggleTaskDone(task.id)">Toggle done</button>
    <button @click="deleteTask(task.id)">Delete task</button>
  </div>
</template>

<script>
import moment from "moment";

export default {
  name: "UserTask",
  props: {
    task: Object
  },
  methods: {
    parseDate() {
      return moment(this.time).format("LL");
    },
    deleteTask(id){
      if (confirm(`Are you sure you want to delete task: ${this.task.name}?`)){
        this.$emit("delete-task", id);
      }
    },
    toggleTaskDone(id) {
      this.$emit("toggle-done", id)
    }
  }
}
</script>

<style scoped>
.task-box {
  font-size: 1.5rem;

  display: flex;
  flex-direction: column;
  justify-content: center;

  margin-bottom: 2rem;
}

button {
  width: 15rem;
}
</style>