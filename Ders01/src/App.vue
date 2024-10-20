<script setup>
import { ref } from 'vue'
import { reactive } from 'vue'
import Header from '@/components/Globals/AppHeader.vue'
const name = ref('Onur')

const user = reactive({
  name: name.value,
  age: 25,
  email: 'onur@example.com',
  address: {
    street: '123 Main St',
    city: 'New York',
    state: 'NY'
  }
})

const handleClick = () => {
  name.value = 'John'
  user.name = name.value
  console.log('Button clicked!')
}
</script>

<template>
  <Header :user="user" :handleClick="handleClick" />
  <h1>Hello, {{ name }}!</h1>

  <app-footer />
</template>

<style scoped></style>
