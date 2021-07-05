<template>
  <div class="task-box">
    <div :class="[task.done ? 'done-task' : '','task-details']">
      <h3>{{ task.name }}</h3>
      <span>{{ task.description }}</span>
      <span>{{ parseDate() }}</span>
      <span>{{ `This task is ${task.done ? "" : "not"} done` }}</span>
    </div>
    <div class="button-box">
      <button @click="toggleTaskDone(task.id)">Toggle done</button>
      <button @click="deleteTask(task.id)">Delete task</button>
    </div>
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
h3 {
  margin: 0;
}

.task-box {
  display: flex;
  flex-direction: row;
  margin-bottom: 1rem;

  justify-content: space-evenly;
  align-items: center;
}

.task-details {
  font-size: 1.5rem;
  width: 40rem;

  display: flex;
  flex-direction: column;
}

.done-task {
  border-left: 3px solid green;
}

.button-box {
  height: 5rem;

  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

.button-box button {
  width: 15rem;
}
</style>