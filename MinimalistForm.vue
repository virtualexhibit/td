<template>
  <form @submit.prevent="addTodo">
    <TextInput
      v-model="task"
      @submit="addTodo"
      :item="{ display: { text: merged.display.title, buttonText: merged.display.buttonText } }"
    />

  </form>
</template>

<script>
import TextInput from './TextInput.vue'
import { FORM_RECIPE } from '../Recipes/rMinimalistForm.js'

export default {
  name: 'MinimalistForm',
  components: { TextInput },
  props: {
    item: { type: Object, default: () => ({}) },
  },
  data() {
    return {
      task: '',
    }
  },
  computed: {
    merged() {
      return {
        display: {
          ...FORM_RECIPE.display,
          ...this.item.display,
        },
        validation: {
          ...FORM_RECIPE.validation,
          ...this.item.validation,
        },
      }
    },
  },
  methods: {
    addTodo() {
      if (!this.task.trim()) return
      this.$emit('add-todo', this.task)
      this.task = ''
    },
  },
}
</script>
