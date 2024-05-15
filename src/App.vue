<script setup>
import { ref, computed } from "vue";

const current = ref('');
const operand = ref('');
const result = ref(0);

const buttons = [
  { label: '7', value: 7 },
  { label: '8', value: 8 },
  { label: '9', value: 9 },
  { label: '\u00F7', value: '/' },
  { label: '4', value: 4 },
  { label: '5', value: 5 },
  { label: '6', value: 6 },
  { label: '\u00d7', value: '*' },
  { label: '1', value: 1 },
  { label: '2', value: 2 },
  { label: '3', value: 3 },
  { label: '-', value: '-' },
  { label: '0', value: 0 },
  { label: '\u2022', value: '.' },
  { label: '=', value: '=' },
  { label: '+', value: '+' },
]

function handleButtonClick(button) {

  if (typeof button.value  === "number") {
    current.value += button.value
    console.log("Hi 1")

  } else {
    console.log("Hi 2")

    switch(operand.value) {

      case '+':
        console.log("Hi 3")
        result.value += parseFloat(current.value); 
        current.value = "";
        break;
      case '-':
        console.log("Hi 4")
        result.value -= parseFloat(current.value)
        current.value = "";
        break;
      case '*':
        result.value *= parseFloat(current.value)
        current.value = "";
        break;
      case '/':
        if(current.value != 0){
          result.value /= parseFloat(current.value)
          current.value = "";
        } else {
          alert('Cannot divide by zero')
        }
        break;
    }
  
 console.log("Hi 5")
  operand.value = button.value
    
  }
   
}

</script>

<template>

<div class="calculator">
  <div class="screen">
    <div class="pevious-operand">{{ result || ''}} {{ operand }} {{current || 0}}</div>
    <div class="current-operand">{{ current || 0}}</div>
  
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
  width: 400px;
  border-radius: 1rem;
  padding: 1.5rem;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  background-color: rgb(87, 87, 87);
  border: 5px solid rgb(66, 66, 66);
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
  
.screen {
  width: 100%;
  background-color: rgb(188, 208, 192);
  border-bottom: 5px solid rgb(156, 171, 159);
  border-radius: .5rem;
  box-shadow: inset 0px 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 1.75rem;

  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  flex-direction: column;
  padding: .5rem;

  word-wrap: break-word;
  word-break: break-all;
}

.pevious-operand {
  opacity: .7;
  font-size: 1rem;
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

  font-weight:bold;
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

/* mobile */
@media (max-width:740px) {
  .calculator {
     max-width: 80%;
  }
  
}

 
  
</style>
