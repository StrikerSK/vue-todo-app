<template>
  <div id="app">
    <h1>Vue Todo Application</h1>
    <div id="form-div">
      <UserButton v-bind:button-text="this.showAddTask ? 'Close' : 'Add task'" @btn-click="toggleShowAddTask"/>
      <UserTaskForm @add-task="addTask" v-show="showAddTask"/>
    </div>
    <div id="task-list">
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
import UserButton from "@/components/UserButton";

export default {
  name: 'App',
  components: {
    UserButton,
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
          description: "Todo with description",
          time: moment().format(),
          done: false
        }
      ],
      showAddTask: false
    }
  },
  methods: {
    increaseValue() {
      this.count = this.count + 1;
    },
    addTask(task) {
      this.tasks = [...this.tasks, task];

      if (!confirm("Task added! Do you want to add new one?")) {
        this.toggleShowAddTask();
      }
    },
    toggleDone(taskID) {
      const taskIndex = this.tasks.findIndex(({id}) => id === taskID);
      this.tasks[taskIndex].done = !this.tasks[taskIndex].done
    },
    deleteTask(taskID) {
      this.tasks = this.tasks.filter(({id}) => id !== taskID);
    },
    toggleShowAddTask() {
      this.showAddTask = !this.showAddTask;
    }
  }
}
</script>

<style>
body {
  margin: 0 !important;
}

html {
  font-size: 62.5%;
}

h1 {
  font-size: 6rem;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  min-height: 100vh;
  width: 100vw;

  display: flex;
  flex-direction: column;
}

#form-div {
  display: flex;
  flex-direction: column;
  justify-content: center;

  align-items: center;
  margin-bottom: 2.5rem;
}

#task-list{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: center;
}
</style>
