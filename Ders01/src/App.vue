<script setup>
import { ref } from 'vue'

const firstMessage = ref('first message')
const links = 'https://google.com'
const newValue = ref('')
const counter = ref(0)

const changeValue = () => {
  firstMessage.value = 'updated message'
}
</script>

<template>
  <header>
    <div class="wrapper">
      <h1>{{ firstMessage }}</h1>
      <h1>{{ newValue }}</h1>
      <a :href="links" target="_blank">Google</a>
      <input v-model="newValue" />
      <button @click="changeValue">Change Message</button>

      <h1>Sayaç</h1>
      <button @click="counter++">Arttır</button>
      <button @click="counter--">Azalt</button>
    </div>
  </header>
</template>

<style scoped></style>
