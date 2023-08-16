<template>
    <h1>Calculator</h1>

    <div class="calculator">
        <div class="display">
            
            <p>Result is {{ displayValue }}</p>
        </div>

        <div class="buttons">

            <div class="row">
                <div class="buttons">
                    <div class="row">
                        <button @click="clearDisplay">C</button>
                        <button @click="appendToDisplay('0')">0</button>
                        <button @click="appendToDisplay('.')">.</button>
                        <button @click="performOperation('-')">-</button>
                        <button @click="calculateResult">=</button>
                    </div>
                
                    <div class="row">
                        <button @click="appendToDisplay('7')">7</button>
                        <button @click="appendToDisplay('8')">8</button>
                        <button @click="appendToDisplay('9')">9</button>
                        <button @click="performOperation('/')">÷</button>
                    </div>
                    <div class="row">
                        <button @click="appendToDisplay('4')">4</button>
                        <button @click="appendToDisplay('5')">5</button>
                        <button @click="appendToDisplay('6')">6</button>
                        <button @click="performOperation('*')">x</button>
                    </div>
                    <div class="row">
                        <button @click="appendToDisplay('1')">1</button>
                        <button @click="appendToDisplay('2')">2</button>
                        <button @click="appendToDisplay('3')">3</button>
                        <button @click="performOperation('+')">+</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script setup>
    import { ref } from 'vue';

    const displayValue = ref('0');
    const currentValue = ref(null);
    const operator = ref(null);

    const appendToDisplay = (value) => {
    if (displayValue.value === '0' || displayValue.value === 'Error') {
        displayValue.value = value;
    } else {
        displayValue.value += value;
    }
    };

    const performOperation = (newOperator) => {
    operator.value = newOperator;
    currentValue.value = parseFloat(displayValue.value);
    displayValue.value = '0';
    };

    const calculateResult = () => {
    if (operator.value && currentValue.value !== null) {
        const newValue = parseFloat(displayValue.value);
        switch (operator.value) {
        case '+':
            displayValue.value = (currentValue.value + newValue).toString();
            break;
        case '-':
            displayValue.value = (currentValue.value - newValue).toString();
            break;
        case '*':
            displayValue.value = (currentValue.value * newValue).toString();
            break;
        case '/':
            if (newValue !== 0) {
            displayValue.value = (currentValue.value / newValue).toString();
            } else {
            displayValue.value = 'Error';
            }
            break;
        }
        operator.value = null;
        currentValue.value = null;
    }
    };

    const clearDisplay = () => {
        displayValue.value = '0';
        operator.value = null;
        currentValue.value = null;
    };
</script>
  
<style scoped>

</style>
