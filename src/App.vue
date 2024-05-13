<script setup>
import { ref } from "vue";

const display = ref(0);
const currentInput = ref(0);
const previousInput = ref(null);
const operator = ref(null);
const buttons = [
  { label: '7', value: '7' },
  { label: '8', value: '8' },
  { label: '9', value: '9' },
  { label: '/', value: '/' },
  { label: '4', value: '4' },
  { label: '5', value: '5' },
  { label: '6', value: '6' },
  { label: '*', value: '*' },
  { label: '1', value: '1' },
  { label: '2', value: '2' },
  { label: '3', value: '3' },
  { label: '-', value: '-' },
  { label: '0', value: '0' },
  { label: '.', value: '.' },
  { label: '=', value: '=' },
  { label: '+', value: '+' },
]


</script>

<template>

<div class="calculator">
  <div class="screen">{{ display }}</div>
  <div class="buttons">
    <button v-for="button in buttons" :key="button.value" @click="handleButtonClick(button)">
      {{ button.label }}
    </button>
  </div>
</div>

</template>

<style scoped>
.calculator {
  width: 400px;
  max-width: 80%;
  border-radius: 1rem;
  padding: 1.5rem;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  background-color: rgb(87, 87, 87);
  border: 5px solid rgb(66, 66, 66);
}
  
.screen {
  width: 100%;
  height: 60px;
  background-color: rgb(188, 208, 192);
  border-bottom: 3px solid rgb(156, 171, 159);
  text-align: right;
  padding: 5px;
  font-size: 18px;
  border-radius: .5rem;
  margin-bottom: 10px;
  box-shadow: inset 0px 2px 4px rgba(0, 0, 0, 0.1);
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 5px;
}

button {
  width: 100%;
  height: 40px;
  background-color: #fff;
  color: rgb(87, 87, 87);
  border: 2px solid rgb(234, 229, 223);
  border-radius: .75rem;
  cursor: pointer;
  transition: background-color 0.2s ease;

  font-weight: bold;
  font-size: 2rem;
  display: grid;
  place-content: center;
}

.bg-red {
  background-color: rgb(248, 106, 111);
  color: white;
}

button:hover {
  background-color: #e2e2e2;
  border-color: white;
}

button:active {
  background-color: #d0d0d0;
}
  
  
</style>
