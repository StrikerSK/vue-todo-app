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
      <button type="submit" v-on:click="printValue">Save task</button>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
import moment from 'moment'

export default {
  name: "UserTaskForm",
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
    }
  }
}
</script>

<style scoped>
.task-form-box {
  margin-bottom: 5rem;
}

.task-form {
  width: 50rem;
  height: 7.5rem;
  margin: 0 auto;
  font-size: 1.5rem;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.task-form div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 60%;
}

button {
  background-color: bisque;
  border: 1px solid black;
  border-radius: 1.2rem;
  width: 12.5rem;
  height: 2rem;
}
</style>