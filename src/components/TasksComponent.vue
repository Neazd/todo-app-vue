<template>
  <div class="tasks-container">
    <ul class="tasks-list">
      <li v-for="(item, index) in items" :key="index" class="task-item">
        <input v-model="isChecked" type="checkbox" class="task-checkbox"/>
        <div v-if="!item.editing" :class="{'strikethrough': isChecked}" class="task-text">
          {{ item.text }}
        </div>
        <input v-if="item.editing" v-model="item.newText" @keyup.enter="finishEditing(item, index)" class="task-input"/>
        <div class="task-buttons">
          <button v-if="!item.editing" @click="editTask(item)" class="task-button small">Edit</button>
          <button v-if="item.editing" @click="finishEditing(item, index)" class="task-button small">Save</button>
          <button @click="deleteItem(index)" class="task-button small">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TasksComponent',
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      isChecked: false,
    };
  },
  methods: {
    deleteItem(index) {
      this.$emit('delete-item', index);
    },
    editTask(item) {
      item.editing = true;
      item.newText = item.text;
    },
    finishEditing(item) {
      item.editing = false;
      if (item.text !== item.newText) {
        this.$emit('update-item', { newText: item.newText, originalText: item.text });
      }
    }
  },
};
</script>

<style>
.tasks-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.tasks-list {
  list-style-type: none;
  padding: 0;
  width: 100%;
}

.task-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.task-checkbox {
  margin-right: 10px;
}

.task-text {
  flex-grow: 1;
}

.strikethrough {
  text-decoration: line-through;
}

.task-input {
  flex-grow: 1;
  margin-right: 10px;
}

.task-buttons {
  display: flex;
  gap: 10px;
}

.task-button {
  padding: 5px 5px;
  margin: 10px;
  border: none;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

.task-button.small {
  padding: 3px 8px;
  font-size: 0.8em;
}

.task-button:hover {
  background-color: #0056b3;
}
</style>
