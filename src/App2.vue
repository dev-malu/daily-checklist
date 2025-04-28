<script setup lang="ts">
import { ref, computed } from 'vue';

//counter
const counter = ref(0);
const incCount = () => {
  counter.value++;
}
const decCount = () => {
  if (counter.value > 0)
    counter.value--;
}

//color finder
const color = ref('blue');

const changeColor = computed(() => {
  return `<span style="color: ${color.value}">This is ${color.value}</span>`
});

//color picker
const selectedColor = ref('');

//pick 4 colors
const selectedColorPalatte = ref([]);
const pickColor = ref('');

const pickColors = () => {
  console.log(selectedColorPalatte.value);
  if (selectedColorPalatte.value.length >= 4) {
    selectedColorPalatte.value.splice(0, 1);
  }
  selectedColorPalatte.value.push(pickColor.value);
}
</script>

<template>
  <div class="counterContainer">
    <h2>Counter</h2>
    <div class="counter">
      <button @click="incCount">+</button>
      <button>Count:{{ counter }} </button>
      <button @click="decCount">-</button>
    </div>
  </div>

  <div class="colorFindContainer">
    <h2>Color Finder</h2>
    <div class="colorFind">
      <input type="text" placeholder="Type color" v-model="color">
      <p v-html="changeColor"></p>
    </div>
  </div>

  <div>
    <h3>Color picker</h3>
    <div>
      <input type="color" v-model="selectedColor">
      <p :style="{ color: selectedColor }">This is {{ selectedColor }}</p>
    </div>
  </div>

  <div>
    <h2>Pick 4 colors</h2>
    <div>
      <input type="color" v-model="pickColor" @change="pickColors()">
      <div>
        <h3>Selected colors</h3>
        <div v-for="(colorValPal, index) in selectedColorPalatte" :key="index" :style="{
          backgroundColor: colorValPal,
          width: '50px',
          height: '50px',
          display: 'inline-block',
          margin: '5px',
          borderRadius: '8px',
          boxShadow: '0 2px 8px rgba(0, 0, 0, 0.2)'
        }"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.counterContainer {

  border: 0.2px solid grey;
  padding: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

button {
  padding: 8px;
}

.counter {
  display: flex;
  gap: 10px;
}
</style>
