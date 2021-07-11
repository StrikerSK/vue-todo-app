<template>
  <div class="task-form-box">
    <form class="task-form">
      <div>
        <label for="taskName">Task name</label>
        <input id="taskName" name="taskName" type="text" v-model="name" />
      </div>
      <div>
        <label for="description">Task description</label>
        <input id="description" name="description" type="text" v-model="description" />
      </div>
      <div id="button-box">
        <button type="submit" v-on:click="printValue">Save task</button>
        <UserButton button-text="Clear" @btn-click="clearData()"/>
      </div>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
import moment from 'moment'
import UserButton from "@/components/UserButton";

export default {
  name: "UserTaskForm",
  components: {UserButton},
  props: {
    addForm: Function
  },
  data() {
    return {
      id: "",
      name: "",
      description: ""
    }
  },
  methods: {
    printValue(e) {
      e.preventDefault();

      if (!this.name) {
        alert("Task name not defined!");
        return;
      }

      const newTask = {
        id: uuidv4(),
        name: this.name,
        description: this.description,
        time: moment().format(),
        done: false
      }

      this.$emit("add-task", newTask);

      this.name = "";
      this.description = "";
      this.id = "";
    },
    clearData() {
      this.name = "";
      this.description = "";
      this.id = "";
    }
  }
}
</script>

<style scoped>
.task-form-box {
  width: 45%;
  margin-top: 1rem;
  padding: 1rem 0;
  border-radius: 3rem;
  background-color: lightgrey;
}

.task-form {
  width: 90%;
  height: 7.5rem;
  margin: 0 auto;
  font-size: 1.5rem;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.task-form div {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

@media (max-width: 420px) {
  .task-form-box {
    width: 95%;
  }
}

.task-form label {
  width: 33.3%;
  text-align: left;
}

.task-form input {
  width: 66.7%;
}

button {
  background-color: bisque;
  border: 1px solid black;
  border-radius: 1.2rem;
  width: 12.5rem;
  height: 2rem;
}

#button-box {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}
</style>