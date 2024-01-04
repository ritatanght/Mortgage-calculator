<script>
import Input from "./components/Input.vue";
import Display from "./components/Display.vue";

export default {
  data() {
    return {
      fields: {
        price: { label: "Purchase price", value: 450000, unit: "$" },
        downPymt: { label: "Down payment", value: 135000, unit: "$" },
        period: { label: "Repayment time", value: 25, unit: " years" },
        rate: { label: "Interest Rate", value: 3, unit: "%" },
      },
      loan: { label: "Loan amount", value: 0 },
      mthPayment: { label: "Estimated pr. month", value: 0 },
    };
  },
  methods: {
    calculateLoanAmt() {
      const price = this.fields.price.value;
      const downPymt = this.fields.downPymt.value;
      this.loan.value = price - downPymt;
    },
    calculatePymt() {
      const loan = this.loan.value;
      const r = this.fields.rate.value / 100 / 12;
      const n = this.fields.period.value * 12;
      this.mthPayment.value =
        loan * r * (Math.pow(1 + r, n) / (Math.pow(1 + r, n) - 1));
    },
  },
  mounted() {
    this.calculateLoanAmt();
    this.calculatePymt();
  },
  watch: {
    fields: {
      handler() {
        this.calculateLoanAmt();
        this.calculatePymt();
      },
      deep: true,
    },
  },
  components: {
    Input,
    Display,
  },
};
</script>

<template>
  <h1>Mortgage calculator</h1>
  <main>
    <Input v-for="field in fields" :input="field" />
    <Display :label="loan.label" :value="loan.value" />
    <Display :label="mthPayment.label" :value="mthPayment.value" />
  </main>
</template>

<style scoped></style>
