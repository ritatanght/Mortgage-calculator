<script>
import Input from "./components/Input.vue";
import Display from "./components/Display.vue";

export default {
  data() {
    return {
      fields: {
        price: {
          label: "Purchase price",
          value: 450000,
          unit: "$",
          step: 1000,
          max: 1000000,
        },
        downPymt: {
          label: "Down payment",
          value: 135000,
          unit: "$",
          step: 1000,
          max: 1000000,
        },
        period: {
          label: "Repayment time",
          value: 25,
          unit: " years",
          step: 1,
          max: 30,
        },
        rate: {
          label: "Interest Rate",
          value: 3,
          unit: "%",
          step: 1,
          max: 10,
        },
      },
      loan: { label: "Loan amount", value: 0 },
      mthPayment: { label: "Est. monthly payment", value: 0 },
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
        if (this.fields.downPymt.value > this.fields.price.value) {
          alert("Down payment cannot be larger than the purchase price");
          this.loan.value = " -- ";
          this.mthPayment.value = " -- ";
        } else {
          this.calculateLoanAmt();
          this.calculatePymt();
        }
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
  <h1>Mortgage Calculator</h1>
  <main>
    <Input v-for="field in fields" :input="field" />
    <Display :label="loan.label" :value="loan.value" />
    <Display :label="mthPayment.label" :value="mthPayment.value" />
  </main>
</template>

<style scoped>
h1 {
  text-align: center;
  padding-bottom: 0.5em;
  border-bottom: 2px solid;
}

main {
  padding: 2em;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 2.5em;
  row-gap: 4em;
}

@media (max-width: 700px) {
  main {
    padding: 1em;
    grid-template-columns: repeat(2, 1fr);
    text-align: center;
    row-gap: 2.5em;
  }
}
</style>
