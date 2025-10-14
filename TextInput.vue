<template>
  <div class="input-group my-3">
    <span class="input-group-text" v-if="merged.display?.text">
      {{ merged.display.text }}
    </span>

    <input
      v-bind="merged.directives"
      v-model="inputValue"
    />

    <button
      class="btn btn-primary"
      type="button"
      @click="$emit('submit', inputValue)"
    >
      {{ merged.display?.buttonText || 'Submit' }}
    </button>
  </div>
</template>

<script>
import { INPUT_RECIPE } from '../Recipes/rTextInput.js'

export default {
  name: 'TextInput',
  props: {
    item: { type: Object, default: () => ({}) },
    modelValue: { type: String, default: '' },
  },
  computed: {
    merged() {
      return {
        directives: {
          ...INPUT_RECIPE.directives,
          ...this.item.directives,
        },
        display: {
          ...INPUT_RECIPE.display,
          ...this.item.display,
        },
      }
    },
    inputValue: {
      get() {
        return this.modelValue
      },
      set(val) {
        this.$emit('update:modelValue', val)
      },
    },
  },
}
</script>
