<template>
  <div class="container mt-5">
    <h2>Interactive Calculator</h2>
    <OperationSelector @selectedOperation="setOperation" />
    <InputFields v-if="operation" :operation="operation" @valuesEntered="calculate" />
    <Result v-if="result !== null" :result="result" />
    <Error v-if="errorMessage" :message="errorMessage" />
  </div>
</template>

<script>
import OperationSelector from './components/OperationSelector.vue';
import InputFields from './components/InputFields.vue';
import Result from './components/Result.vue';
import Error from './components/Error.vue';

export default {
  data() {
    return {
      operation: '',
      result: null,
      errorMessage: '',
    };
  },
  components: {
    OperationSelector,
    InputFields,
    Result,
    Error,
  },
  methods: {
    setOperation(op) {
      this.operation = op;
      this.result = null;
      this.errorMessage = '';
    },
    calculate({ value1, value2 }) {
      const num1 = parseFloat(value1);
      const num2 = parseFloat(value2);

      if (isNaN(num1) || isNaN(num2)) {
        this.errorMessage = 'Please enter valid numbers';
        this.result = null;
        return;
      }

      switch (this.operation) {
        case 'add':
          this.result = num1 + num2;
          break;
        case 'subtract':
          this.result = num1 - num2;
          break;
        case 'multiply':
          this.result = num1 * num2;
          break;
        case 'divide':
          if (num2 === 0) {
            this.errorMessage = 'Cannot divide by zero';
            this.result = null;
            return;
          }
          this.result = num1 / num2;
          break;
        default:
          this.errorMessage = 'Unknown operation';
      }

      this.errorMessage = '';
    },
  },
};
</script>
