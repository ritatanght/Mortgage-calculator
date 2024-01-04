<script>
export default {
  props: {
    input: Object,
    //{ label: String, value: Number, unit: String },
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
    <label :for="input.label.split(' ').join('-')">{{ input.label }}:</label>
    <strong>{{
      input.unit === "$" ? input.unit + input.value : input.value + input.unit
    }}</strong>
    <input
      type="range"
      :id="input.label.split(' ').join('-')"
      v-model="input.value"
      min="1"
      :max="maxValue()"
    />
  </div>
</template>

<style scoped></style>
