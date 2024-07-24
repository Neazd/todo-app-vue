<template>
  <div id="app">
    <h1>Task List</h1>
    <div>
      <form @submit.prevent="submitForm">
        <input type="text" v-model="newTask" placeholder="Enter a task" />
        <button type="submit">Add Task</button>
      </form>
    </div>
    <TasksComponent :items="tasks" @update-items="updateItems" @delete-item="deleteTask"/>
  </div>
</template>

<script>
import TasksComponent from "./components/TasksComponent.vue";

export default {
  name: "App",
  components: {
    TasksComponent,
  },
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    submitForm() {
      if (this.newTask) {
        this.tasks.push(this.newTask);
        this.newTask = "";
      }
    },
    updateItems(newTasks) {
      this.tasks = newTasks;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  },
};
</script>

<style>
/* Add your styles here */
</style>
