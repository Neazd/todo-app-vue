<template>
  <div id="app" class="app-container">
    <h1 class="app-title">Task List</h1>
    <div class="form-container">
      <form @submit.prevent="submitForm" class="task-form">
        <input type="text" v-model="newTask" placeholder="Enter a task" class="task-input"/>
        <button type="submit" class="task-button small">Add Task</button>
      </form>
    </div>
    <TasksComponent :items="tasks" @update-item="updateTask" @delete-item="deleteTask"/>
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
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask, editing: false });
        this.newTask = "";
      }
    },
    updateTask(updatedItem) {
      const index = this.tasks.findIndex(task => task.text === updatedItem.originalText);
      if (index !== -1) {
        this.tasks[index].text = updatedItem.newText;
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  },
};
</script>

<style>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.app-title {
  font-size: 2em;
  margin-bottom: 20px;
}

.form-container {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.task-form {
  display: flex;
  gap: 10px;
}

.task-input {
  padding: 10px;
  font-size: 1em;
  width: 300px;
}

.task-button {
  padding: 10px 20px;
  font-size: 1em;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}

.task-button.small {
  padding: 5px 10px;
  font-size: 0.8em;
}

.task-button:hover {
  background-color: #0056b3;
}
</style>
