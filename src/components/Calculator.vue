<template>
  <div class="card p-4 shadow-sm">
    <h4 class="mb-3 text-center">Choisissez une opération</h4>
    <div class="mb-2" v-for="op in operations" :key="op.value">
      <input 
        class="form-check-input" 
        type="radio" 
        :id="op.value" 
        :value="op.value" 
        v-model="operation"
      />
      <label class="form-check-label ms-2" :for="op.value">{{ op.label }}</label>
    </div>

    <h4 class="mt-4 mb-3 text-center">Saisissez les valeurs</h4>
    <div class="mb-3">
      <input 
        type="number" 
        v-model="value1" 
        placeholder="Valeur 1" 
        class="form-control" 
        :class="{'is-invalid': error.value1}"
      />
      <div v-if="error.value1" class="invalid-feedback">{{ error.value1 }}</div>
    </div>
    <div class="mb-3">
      <input 
        type="number" 
        v-model="value2" 
        placeholder="Valeur 2" 
        class="form-control" 
        :class="{'is-invalid': error.value2}"
      />
      <div v-if="error.value2" class="invalid-feedback">{{ error.value2 }}</div>
    </div>

    <button class="btn btn-primary w-100" @click="calculate">Calculer</button>

    <div v-if="error.general" class="text-danger mt-3">{{ error.general }}</div>
    <div v-if="result !== null" class="alert alert-success mt-3">Résultat: {{ result }}</div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const operations = [
  { label: 'Addition', value: 'addition' },
  { label: 'Soustraction', value: 'subtraction' },
  { label: 'Multiplication', value: 'multiplication' },
  { label: 'Division', value: 'division' }
];

const value1 = ref(null);
const value2 = ref(null);
const operation = ref('addition'); // Par défaut, l'opération est "addition"
const result = ref(null);
const error = ref({
  value1: '',
  value2: '',
  general: ''
});

// Fonction pour effectuer le calcul
const calculate = () => {
  // Réinitialisation des erreurs
  error.value1 = '';
  error.value2 = '';
  error.general = '';
  result.value = null;

  // Validation des champs
  if (!value1.value) {
    error.value1 = 'Valeur 1 est obligatoire';
  }
  if (!value2.value) {
    error.value2 = 'Valeur 2 est obligatoire';
  }

  if (error.value1 || error.value2) {
    return;
  }

  // Conversion des valeurs en nombre
  const num1 = parseFloat(value1.value);
  const num2 = parseFloat(value2.value);

  // Calcul en fonction de l'opération
  if (operation.value === 'addition') {
    result.value = num1 + num2;
  } else if (operation.value === 'subtraction') {
    result.value = num1 - num2;
  } else if (operation.value === 'multiplication') {
    result.value = num1 * num2;
  } else if (operation.value === 'division') {
    if (num2 === 0) {
      error.general = 'Division par zéro non permise';
    } else {
      result.value = num1 / num2;
    }
  }
};
</script>
