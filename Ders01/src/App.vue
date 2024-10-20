<script setup>
import { ref } from 'vue'
import Header from '@/components/Globals/AppHeader.vue'
const name = ref('Onur')

const handleClick = () => {
  name.value = 'John'
  console.log('Button clicked!')
}
</script>

<template>
  <Header />
  <h1>Hello, {{ name }}!</h1>

  <button @click="handleClick">Değiştir</button>

  <app-footer />
</template>

<style scoped></style>
