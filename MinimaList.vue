<template>
  <div class="container mt-4">
    <h2 v-if="merged.showHeader" class="mb-3 text-center">{{ merged.title }}</h2>

    <MinimalistForm @add-todo="addTask" />
    <Buttons
      @clear-completed="clearCompleted"
      @clear-all="clearAll"
    />
    <MinimalistList
      :tasks="tasks"
      @delete-task="deleteTask"
      @toggle-task="toggleTask"
    />

   
  </div>
</template>

<script>
import MinimalistForm from './SubComponents/MinimalistForm.vue'
import MinimalistList from './SubComponents/MinimalistList.vue'
import Buttons from './SubComponents/SomeButtons.vue'
import { MINIMALIST_APP_RECIPE } from './Recipes/rMinimalist.js'

export default {
  name: 'MinimaList',
  components: { MinimalistForm, MinimalistList, Buttons },
  props: {
    item: { type: Object, default: () => ({}) },
  },
  data() {
    return {
      tasks: [],
    }
  },
  computed: {
    merged() {
      return {
        ...MINIMALIST_APP_RECIPE,
        ...this.item,
      }
    },
  },
  methods: {
    addTask(task) {
      this.tasks.push({ text: task, completed: false })
    },
    deleteTask(index) {
      this.tasks.splice(index, 1)
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(task => !task.completed)
    },
    clearAll() {
      this.tasks = []
    },
  },
}
</script>

<style scoped>
.container {
  max-width: 500px;
  
}
</style>
