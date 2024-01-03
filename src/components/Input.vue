<script>
export default {
  props: {
    input: { type: String, label: String, value: Number, unit: String },
  },
};
</script>

<template>
  <div>
    <span
      >{{ input.label }}:
      <strong>{{
        input.unit === "$" ? input.unit + input.value : input.value + input.unit
      }}</strong></span
    >
    <input :type="input.type" v-model="input.value" />
  </div>
</template>

<style scoped></style>
