<template>
  <div id="app">
    <h1>Vue Todo Application</h1>
    <UserTaskForm @add-task="addTask" />
    <div class="task-list">
      <UserTask
          v-bind:key="task.id"
          v-for="task in this.tasks"
          :task="task"
          @toggle-done="toggleDone"
          @delete-task="deleteTask"
      />
    </div>
  </div>
</template>

<script>
import UserTaskForm from "@/components/UserTaskForm";
import UserTask from "@/components/UserTask";
import moment from "moment";

export default {
  name: 'App',
  components: {
    UserTask,
    UserTaskForm
  },
  data() {
    return {
      count: 0,
      tasks: [
          {
            id: "1",
            name: "First todo",
            time: moment().format(),
            done: true
          },
        {
          id: "2",
          name: "Second todo",
          description: "Second todo description",
          time: moment().format(),
          done: false
        }
      ]
    }
  },
  methods: {
    increaseValue() {
      this.count = this.count + 1;
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    toggleDone(taskID) {
      const taskIndex = this.tasks.findIndex(({id}) => id === taskID);
      this.tasks[taskIndex].done = !this.tasks[taskIndex].done
    },
    deleteTask(taskID) {
      this.tasks = this.tasks.filter(({id}) => id !== taskID);
    }
  }
}
</script>

<style>
html {
  font-size: 62.5%;
}

h1 {
  font-size: 5rem;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
