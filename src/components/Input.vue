<script>
export default {
  props: {
    input: Object,
    //{ label: String, value: Number, unit: String,  step: Number, max: Number },
  },
  computed: {
    formattedValue() {
      return this.input.unit === "$"
        ? this.input.unit + this.input.value.toLocaleString("en-CA")
        : this.input.value + this.input.unit;
    },
  },
};
</script>

<template>
  <div>
    <label :for="input.label.split(' ').join('-')">{{ input.label }}: </label>
    <strong>{{ formattedValue }}</strong>
    <input
      type="range"
      :id="input.label.split(' ').join('-')"
      v-model="input.value"
      :min="input.step"
      :max="input.max"
      :step="input.step"
    />
  </div>
</template>

<style scoped>
strong {
  font-size: 1.2rem;
}

input {
  display: block;
  margin-top: 1.5em;
  width: 100%;
  accent-color: #75c9b7;
}

@media (max-width: 700px) {
  strong {
    display: block;
    margin-top: 0.5em;
  }
}
</style>
