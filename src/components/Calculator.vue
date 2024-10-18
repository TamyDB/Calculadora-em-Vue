<script setup>

import { reactive } from 'vue';

const state = reactive({
    firstNum: '',
    secondNum: '',
    mathOperation: 'addition',
    operations: {
        addition: (x, y) => x + y,
        subtraction: (x, y) => x - y,
        multiplication: (x, y) => x * y,
        division: (x, y) => (y !== 0 ? x / y : 'Division by zero'),
    },
    result: 0,
})

const calculateResult = () => {
    const { firstNum, secondNum, mathOperation } = state;
    const num1 = parseFloat(firstNum);
    const num2 = parseFloat(secondNum);

    if (state.operations[mathOperation]) {
        state.result = state.operations[mathOperation](num1, num2);
    }
}
</script>

<template>
    <header>
        <h1 class="pt-4 mb-5 text-center">Calculadora em Vue</h1>
    </header>
    <form>
        <input type="number" class="form-control" v-model="state.firstNum" @input="calculateResult">
        <input type="number" class="form-control mt-5" v-model="state.secondNum" @input="calculateResult">
        <p class="pt-3 text-center">
            Resultado: {{ state.result }}
        </p>
        <select class="form-control mt-5 text-center" v-model="state.mathOperation" @change="calculateResult">
            <option value="addition">Adição</option>
            <option value="subtraction">Subtração</option>
            <option value="multiplication">Multiplicação</option>
            <option value="division">Divisão</option>
        </select>

    </form>
</template>
