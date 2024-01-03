<script>
import Input from "./components/Input.vue";

export default {
  data() {
    return {
      fields: [
        { type: "range", label: "Purchase price", value: 0, unit: "$" },
        { type: "range", label: "Down payment", value: 0, unit: "$" },
        { type: "range", label: "Repayment time", value: 0, unit: " years" },
        { type: "range", label: "Interest Rate", value: 0, unit: "%" },
      ],
    };
  },
  components: {
    Input,
  },
};
</script>

<template>
  <h1>Mortgage calculator</h1>
  <main>
    <Input v-for="field in fields" :input="field" />
  </main>
</template>

<style scoped></style>
