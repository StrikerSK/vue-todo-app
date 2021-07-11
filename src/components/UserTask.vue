<template>
  <div :class="[task.done ? 'done-task' : '', 'task-box']">
    <div class="task-details">
      <h3>{{ task.name }}</h3>
      <span :id="[!task.description ? 'no-desc' : '']">{{ !task.description ? "No description" : task.description }}</span>
      <span>{{ parseDate() }}</span>
      <span>{{ `This task is ${task.done ? "" : "not"} done` }}</span>
    </div>
    <div class="button-box">
      <UserButton button-text="Toggle done" @btn-click="toggleTaskDone(task.id)"/>
      <UserButton button-text="Delete task" @btn-click="deleteTask(task.id)"/>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import UserButton from "@/components/UserButton";

export default {
  name: "UserTask",
  components: {UserButton},
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
  flex-direction: column;
  margin-bottom: 1rem;

  padding-top: 1rem;
  padding-bottom: 1rem;

  border-left: solid 0.25rem red;
  border-radius: 3rem;

  background-color: lightgrey;

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
  border-left: 0.25rem solid green;
}

.button-box {
  width: 80%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

#no-desc {
  color: darkgrey;
}

</style>