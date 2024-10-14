<script setup>
const { todos } = defineProps({
  todos: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <div>
    <li v-for="(todo, index) in todos" :key="index">
      {{ todo.text }}
    </li>
  </div>
</template>

<style scoped></style>
