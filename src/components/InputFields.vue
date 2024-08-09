<template>
  <div class="mb-3">
    <label class="form-label">Enter Values:</label>
    <input type="number" class="form-control mb-2" v-model="value1" placeholder="First value" />
    <input type="number" class="form-control mb-2" v-model="value2" placeholder="Second value" />
    <button class="btn btn-success" @click="emitValues">Calculate</button>
  </div>
</template>

<script>
export default {
  props: ['operation'],
  data() {
    return {
      value1: '',
      value2: '',
    };
  },
  methods: {
    emitValues() {
      this.$emit('valuesEntered', { value1: this.value1, value2: this.value2 });
    },
  },
};
</script>
