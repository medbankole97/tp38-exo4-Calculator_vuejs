<template>
  <div class="alert alert-danger mt-3">
    <strong>Error:</strong> {{ message }}
  </div>
</template>

<script>
export default {
  props: ['message'],
};
</script>
