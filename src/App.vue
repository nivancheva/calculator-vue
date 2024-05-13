<script setup>
import { ref, computed } from "vue";

const display = ref(0);
const currentInput = ref(0);
const previousInput = ref(null);
const operator = ref(null);
const buttons = [
  { label: '7', value: '7' },
  { label: '8', value: '8' },
  { label: '9', value: '9' },
  { label: '÷', value: '/' },
  { label: '4', value: '4' },
  { label: '5', value: '5' },
  { label: '6', value: '6' },
  { label: '×', value: '*' },
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
  <div class="screen">
    <div class="pevious-operand">{{ display }}</div>
    <div class="current-operand">{{ display }}</div>
  </div>
  
  <div class="buttons">
    <button :class="{ 'bg-red' : button.label === '='}" v-for="button in buttons" :key="button.value" @click="handleButtonClick(button)">
      {{ button.label }}
    </button>
  </div>
</div>

</template>

<style scoped>
.calculator {
  width: 450px;
  max-width: 80%;
  border-radius: 1rem;
  padding: 1.5rem;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  background-color: rgb(87, 87, 87);
  border: 5px solid rgb(66, 66, 66);
}
  
.screen {
  width: 100%;
  background-color: rgb(188, 208, 192);
  border-bottom: 3px solid rgb(156, 171, 159);
  border-radius: .5rem;
  box-shadow: inset 0px 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 1.75rem;

  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  flex-direction: column;
  padding: .75rem;

  word-wrap: break-word;
  word-break: break-all;
}

.pevious-operand {
  opacity: .7;
  font-size: 1.5rem;
}

.current-operand {
  font-size: 2.5rem;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: .75rem;
}

button {
  width: 100%;
  background-color: #fff;
  color: rgb(87, 87, 87);
  border: 2px solid rgb(234, 229, 223);
  border-radius: .75rem;
  cursor: pointer;
  transition: background-color 0.2s ease;

  font-weight: bold;
  font-size: 2.5rem;
  display: grid;
  place-content: center;
}

.bg-red {
  background-color: rgb(248, 106, 111);
  color: white;
}

.bg-red:hover {
  background-color: rgb(252, 76, 82);
}

.bg-red:active {
  background-color: rgb(250, 50, 57);
}

button:hover {
  background-color: #e2e2e2;
  border-color: white;
}

button:active {
  background-color: #d0d0d0;
}
  
  
</style>
