<script setup>
import { ref } from 'vue'

const firstBox = ref(false)
const secondBox = ref(false)
const chooseBoxStyle = (number) => {
  console.log(number)
  if (number === '1') {
    firstBox.value = !firstBox.value
  } else if (number === '2') {
    secondBox.value = !secondBox.value
  }
}
</script>

<template>
  <header>
    <div class="wrapper">
      <div class="box" :class="{ selected: firstBox }" @click="chooseBoxStyle('1')"></div>
      <div
        class="box"
        @click="chooseBoxStyle('2')"
        :style="{ borderColor: secondBox ? 'darkmagenta' : 'gray' }"
      ></div>
    </div>
  </header>
</template>

<style scoped>
.box {
  width: 200px;
  height: 200px;
  transition: background-color 0.5s;
  margin: 10px;
  border: dashed;
}

.selected {
  border-color: darkmagenta;
}
</style>
