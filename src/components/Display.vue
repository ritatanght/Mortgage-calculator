<script>
export default {
  props: {
    label: String,
    value: Number | String,
    //{ label: String, value: Number },
  },
};
</script>

<template>
  <div>
    <p class="label">{{ label }}</p>
    <p>
      ${{
        value % 1 === 0
          ? value.toLocaleString("en-CA")
          : value.toLocaleString("en-CA", { maximumFractionDigits: 2 })
      }}
    </p>
  </div>
</template>

<style scoped>
div {
  font-size: 1.2rem;
}
p.label {
  margin: 0;
  margin-bottom: 1em;
}

p:not(.label) {
  font-size: 1.5rem;
  font-weight: bold;
}
</style>
