<template>
  <div id="result">
    <h1>Result:</h1>
    <h5>Operation Used: {{ this._.startCase(this.setFormData.operation) }}</h5>
    <br />
    <p>{{ setFormData.num1 }} {{ symbol }} {{ setFormData.num2 }}</p>
    <p>={{ setFormData.result }}</p>
  </div>
</template>

<script>
export default {
  props: {
    setFormData: Object,
  },
  computed: {
    symbol() {
      let symbol;
      if (this.setFormData.operation == "addition") {
        symbol = "+";
      } else if (this.setFormData.operation == "subtraction") {
        symbol = "-";
      } else if (this.setFormData.operation == "multiplication") {
        symbol = "×";
      } else if (this.setFormData.operation == "division") {
        symbol = "÷";
      } else if (this.setFormData.operation == "modulo") {
        symbol = "%";
      }
      return symbol;
    },
  },
};
// Addition - Green #397535
// Subtraction - Red #753535
// Multiplication - Blue #354675
// Division - Orange #755235
</script>

<style scoped>
#result {
  color: white;
}

#result p {
  font-size: 50pt;
}
</style>
