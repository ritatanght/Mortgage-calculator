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
  max-height: 120px;
}

p.label {
  margin-bottom: 1em;
}

p:not(.label) {
  font-size: 1.5rem;
  font-weight: bold;
}

@media (max-width: 700px) {
  p.label {
    margin-bottom: 0.8em;
  }
  div {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
}
</style>
