<template>
  <div class="container mt-5">
    <h2>Interactive Calculator</h2>
    
    <!-- Composant pour sélectionner l'opération -->
    <OperationSelector @selectedOperation="setOperation" />
    
    <!-- Composant pour saisir les valeurs -->
    <InputFields v-if="operation" :operation="operation" @valuesEntered="calculate" />
    
    <!-- Composant pour afficher le résultat -->
    <Result v-if="result !== null" :result="result" />
    
    <!-- Composant pour afficher les erreurs -->
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
      operation: '', // Opération sélectionnée par l'utilisateur
      result: null, // Résultat du calcul
      errorMessage: '', // Message d'erreur en cas de problème
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
      this.result = null; // Réinitialiser le résultat
      this.errorMessage = ''; // Réinitialiser le message d'erreur
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

<style scoped>
.container {
  max-width: 500px;
  margin: 0 auto;
}

h2 {
  text-align: center;
  margin-bottom: 2rem;
}
</style>
