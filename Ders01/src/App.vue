<script setup>
import { ref } from 'vue'

const todos = ref([])
const newTodo = ref('')

const addTodo = () => {
  if (newTodo.value) {
    todos.value.push({ text: newTodo.value, completed: false })
  }
}
</script>

<template>
  <header>
    <h3>TODO</h3>
    <input type="text" v-model="newTodo" placeholder="Enter a new TODO" />
    <button @click="addTodo(newTodo)">Add</button>

    <p v-if="todos.length == 0">Todo Bulunmamaktadır</p>
    <p v-else>TODO LİST</p>

    <ul class="todos">
      <li v-for="todo in todos" :key="todo.text">
        {{ todo.text }}
      </li>
    </ul>
  </header>
</template>

<style scoped></style>
