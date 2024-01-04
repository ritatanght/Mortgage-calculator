<script>
export default {
  props: {
    label: String,
    value: Number,
    //{ label: String, value: Number },
  },
};
</script>

<template>
  <div>
    <p>{{ label }}</p>
    <p>${{ value % 1 === 0 ? value : value.toFixed(2) }}</p>
  </div>
</template>

<style scoped></style>
