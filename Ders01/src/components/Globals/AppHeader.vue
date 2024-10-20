<template>
  <header>
    <h3>{{ name }}</h3>
    <p>{{ age }} years old</p>
    <p>{{ email }}</p>
    <p>{{ address.street }}</p>
    <button @click="handleClick">Change Name</button>
  </header>
</template>

<script setup>
const props = defineProps({
  user: Object,
  handleClick: Function
})

const { name, age, email, address } = props.user
</script>

<style scoped></style>
