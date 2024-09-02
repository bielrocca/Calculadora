<script setup>
import { ref, watch } from 'vue';

const currentInput = ref('');
const val = ref('');
const values = ref([]);
const valA = ref(0);
const operator = ref(null);

const handleButtonClick = (value) => {
  if (value === '=') {
    if (operator.value) {
      const result = calculateResult();
      val.value = result;
      valA.value = result;
      operator.value = null;
    } else {
      try {
        val.value = eval(values.value.join(''));
      } catch (error) {
        val.value = 'Error';
      }
    }
    values.value = [];
    currentInput.value = '';
  } else if (value === 'CE') {
    if (values.value.length > 0) {
      values.value.pop();
      updateCurrentInput();
    }
  } else if (value === 'C') {
    values.value = [];
    val.value = '';
    operator.value = null;
    valA.value = 0;
    currentInput.value = '';
  } else if (['+', '-', 'x', '/', '%'].includes(value)) {
    if (operator.value) {
      valA.value = calculateResult();
      values.value = [];
    } else {
      valA.value = parseFloat(values.value.join('')) || 0;
      values.value = [];
    }
    operator.value = value;
    currentInput.value = `${valA.value} ${operator.value} `;
  } else if (value === '+/-') {
    if (values.value.length > 0) {
      const lastIndex = values.value.length - 1;
      values.value[lastIndex] = (parseFloat(values.value[lastIndex]) * -1).toString();
      updateCurrentInput();
    }
  } else if (value === ',') {
    if (values.value.length > 0 && !values.value.includes('.')) {
      values.value.push('.');
      updateCurrentInput();
    }
  } else {
    values.value.push(value);
    updateCurrentInput();
  }
};

const calculateResult = () => {
  const expression = `${valA.value} ${operator.value} ${values.value.join('')}`;
  try {
    return eval(expression.replace('x', '*').replace('÷', '/'));
  } catch {
    return 'Error';
  }
};

const updateCurrentInput = () => {
  currentInput.value = values.value.join('');
  if (operator.value) {
    currentInput.value = `${valA.value} ${operator.value} ${values.value.join('')}`;
  }
  try {
    val.value = eval(currentInput.value.replace('x', '*').replace('÷', '/'));
  } catch {
    val.value = '';
  }
};

watch(currentInput, () => {
  updateCurrentInput();
});
</script>

<template>
  <div class="container">
    <div class="row mt-5">
      <div class="col-12">
        <input type="text" :value="currentInput" readonly />
        <h2>Resultado: {{ val }}</h2>
      </div>
    </div>
    <div class="row">
      <div class="col-3">
        <button @click="handleButtonClick('7')">
          <img src="/Calculadora/sete.png" alt="Botão 7">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('8')">
          <img src="/Calculadora/numero-8.png" alt="Botão 8">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('9')">
          <img src="/Calculadora/numero-9.png" alt="Botão 9">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('+')">
          <img src="/Calculadora/mais.png" alt="Botão +">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('4')">
          <img src="/Calculadora/numero-quatro.png" alt="Botão 4">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('5')">
          <img src="/Calculadora/numero-5.png" alt="Botão 5">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('6')">
          <img src="/Calculadora/seis.png" alt="Botão 6">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('-')">
          <img src="/Calculadora/menos.png" alt="Botão -">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('1')">
          <img src="/Calculadora/numero-um.png" alt="Botão 1">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('2')">
          <img src="/Calculadora/numero-2.png" alt="Botão 2">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('3')">
          <img src="/Calculadora/numero-3.png" alt="Botão 3">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('x')">
          <img src="/Calculadora/asterisco.png" alt="Botão x">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick(',')">
          <img src="/Calculadora/virgula.png" alt="Botão ,">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('0')">
          <img src="/Calculadora/zero.png" alt="Botão 0">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('%')">
          <img src="/Calculadora/por-cento.png" alt="Botão %">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('/')">
          <img src="/Calculadora/golpear.png" alt="Botão /">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('Space')">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('C')">
          <img src="/Calculadora/letra-c.png" alt="Botão C">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('Space')">
        </button>
      </div>
      <div class="col-3">
        <button @click="handleButtonClick('=')">
          <img src="/Calculadora/igual.png" alt="Botão =">
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
button {
  border: none;
  background: transparent;
  padding: 0;
}

img {
  width: 80px;
  height: auto;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 1.5em;
  text-align: right;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 10px;
}
</style>
