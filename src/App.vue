<script setup>
import { ref, computed } from "vue";

const current = ref('');
const operand = ref('');
const result = ref(0);
const calculated = ref(false);

const buttons = [
  { label: '7', value: "7" },
  { label: '8', value: "8" },
  { label: '9', value: "9" },
  { label: '\u00F7', value: '/' },
  { label: '4', value: "4" },
  { label: '5', value: "5" },
  { label: '6', value: "6" },
  { label: '\u00d7', value: '*' },
  { label: '1', value: "1" },
  { label: '2', value: "2" },
  { label: '3', value: "3" },
  { label: '-', value: '-' },
  { label: '0', value: "0" },
  { label: '\u2022', value: '.' },
  { label: 'C', value: 'C' },
  { label: '+', value: '+' },
  { label: '=', value: '=' },
]

function calculate(number) {
  if (!isNaN(number) || number === '.') {
    if (calculated.value == true ) {
      current.value = '' ;
      calculated.value = false;
    }

    if (number === '.' && current.value.includes('.')) {
      return;
    }

    current.value += number;
  
  } else if (number === "C" || number === 'Delete' || number === 'Backspace') { 
      current.value = '';
      result.value = '';
      operand.value = '';
  } else {

    if (operand.value == '') {
      result.value = parseFloat(current.value);
      current.value = ''
    } else if (current.value) {
      switch(operand.value) {
        case '+':
          result.value += parseFloat(current.value); 
          current.value = '';
          break;
        case '-':
          result.value -= parseFloat(current.value);
          current.value = "";
          break;
        case '*':
          result.value *= parseFloat(current.value);
          current.value = "";
          break;
        case '/':
          if(current.value != 0){
            result.value /= parseFloat(current.value);
            current.value = "";
          } else {
            alert('Cannot divide by zero');
            current.value = "";
            return;
          }
          break;
      }
    }

    operand.value = number;
    
  }

  if (number === '=' || number === 'Enter') {
    
    operand.value = '';
    current.value = Math.round(result.value * 100) / 100;
    result.value = '' ;
    calculated.value = true;
    
  }  
}

function numberFromKeyboard(event) {
  calculate(event.key);
}

function numberFromKButton(button) {
  calculate(button.value);
}

</script>

<template>

<div class="calculator" tabindex="0" @keydown="numberFromKeyboard">
  <div class="screen">
    <div class="pevious-operand">{{ result || ''}} {{ operand }}</div>
    <div class="current-operand">{{ current || 0}}</div>  
  </div>
  
  <div class="buttons">
    <button
      :class="{ 'bg-red' : button.label === '='}"
      v-for="button in buttons"
      :key="button.value"
      @click="numberFromKButton(button)">
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
  position: relative;

  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  flex-direction: column;
  padding: 2.5rem .5rem .5rem;

  word-wrap: break-word;
  word-break: break-all;
}

.pevious-operand {
  opacity: .7;
  font-size: 1rem;
  position: absolute;
  right: .5rem;
  top: 1rem;
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
  grid-column: span 4;
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
