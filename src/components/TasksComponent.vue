<template>
  <div>
    <ul>
      <li  v-for="(item, index) in items" :key="index"> <input v-model="isChecked" type="checkbox"/> <div v-if="!item.editing" :class="{'strikethrough': isChecked}">{{ item }} </div><button @click="updateTask(index)">Update Task</button><button @click="deleteItem(index)">Delete</button></li>
    </ul>
  </div>
  <h1>Zmienna jest:{{inputValue}}</h1>
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
  data(){
    return {
      isChecked: false,
    }
  },
  methods: {
    deleteItem(index) {
      this.$emit('delete-item', index);
    },
    updateTask(index){
      this.$emit('update-item', index)
    }
  },
};
</script>

<style>
.strikethrough {
  text-decoration: line-through;
}
</style>
