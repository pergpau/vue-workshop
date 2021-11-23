<template>
  <div class="todo-item">
    <label class="todo-checkbox">
      <input
        type="checkbox"
        :value="isCompleted"
        @input="$emit('check')"
      >
      <span></span>
    </label>
    <div :class="{completed: isCompleted}">{{ text }}</div>
    <span
      class="material-icons"
      @click="$emit('delete')"
    >
      delete
    </span>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps({
  text: String,
  isCompleted: Boolean
})

</script>
