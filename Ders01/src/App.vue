<script setup>
import { ref } from 'vue'

const name = ref('Onur')

const handleClick = () => {
  name.value = 'John'
  console.log('Button clicked!')
}
</script>

<template>
  <h1>Hello, {{ name }}!</h1>

  <button @click="handleClick">Değiştir</button>
</template>

<style scoped></style>
