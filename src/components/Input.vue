<script>
export default {
  props: {
    input: { type: String, label: String, value: Number, unit: String },
  },
  methods: {
    maxValue() {
      switch (this.input.unit) {
        case "$":
          return 1000000;
        case "%":
          return 10;
        case " years":
          return 30;
      }
    },
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
    <input :type="input.type" v-model="input.value" :max="maxValue()"/>
  </div>
</template>

<style scoped></style>
