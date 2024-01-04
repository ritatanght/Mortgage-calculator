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
    <label :for="input.label.split(' ').join('-')">{{ input.label }}: </label>
    <strong>{{
      this.input.unit === "$"
        ? this.input.unit + this.input.value.toLocaleString("en-CA")
        : this.input.value + this.input.unit
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
