<template>
  <div class="text-center mt-3">
    <button
      v-for="(btn, index) in merged.buttons"
      :key="index"
      :class="btn.class"
      @click="$emit(btn.event)"
    >
      {{ btn.text }}
    </button>
  </div>
</template>

<script>
import { BUTTONS_RECIPE } from '../Recipes/rButtons.js'

export default {
  name: 'SomeButtons',
  props: {
    item: { type: Object, default: () => ({}) },
  },
  computed: {
    merged() {
      return {
        ...BUTTONS_RECIPE,
        ...this.item,
      }
    },
  },
}
</script>

<style scoped>
button {
  margin: 0 5px;
}
</style>
