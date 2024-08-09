<template>
  <div class="mb-3">
    <label class="form-label">Select Operation:</label>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="add" value="add" v-model="selectedOperation" />
      <label class="form-check-label" for="add">Addition</label>
    </div>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="subtract" value="subtract" v-model="selectedOperation" />
      <label class="form-check-label" for="subtract">Subtraction</label>
    </div>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="multiply" value="multiply" v-model="selectedOperation" />
      <label class="form-check-label" for="multiply">Multiplication</label>
    </div>
    <div class="form-check">
      <input class="form-check-input" type="radio" id="divide" value="divide" v-model="selectedOperation" />
      <label class="form-check-label" for="divide">Division</label>
    </div>
    <button class="btn btn-primary mt-3" @click="emitOperation">Select</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedOperation: '',
    };
  },
  methods: {
    emitOperation() {
      this.$emit('selectedOperation', this.selectedOperation);
    },
  },
};
</script>
