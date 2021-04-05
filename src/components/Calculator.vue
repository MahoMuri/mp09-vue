<template>
  <div id="calculator">
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group
        id="value1"
        label="Input Number 1: "
        label-for="value1Input"
      >
        <b-form-input
          id="value1Input"
          v-model="form.num1"
          type="number"
          placeholder="Must be a number."
          required
        />
      </b-form-group>

      <b-form-group
        id="operation"
        label="Operation Selected: "
        label-for="operationInput"
      >
        <b-form-select
          id="operationInput"
          v-model="form.operation"
          :options="operations"
          required
        />
      </b-form-group>

      <b-form-group
        id="value2"
        label="Input Number 2: "
        label-for="value2Input"
      >
        <b-form-input
          id="value2Input"
          v-model="form.num2"
          type="number"
          placeholder="Must be a number."
          required
        />
      </b-form-group>
      <b-button type="submit" variant="primary"> Submit </b-button>
      <b-button type="reset" variant="danger"> Reset </b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        num1: null,
        num2: null,
        operation: null,
        result: null,
      },
      operations: [
        {
          value: null,
          text: "Select an Operation",
        },
        {
          // value: "addition",
          value: {
            text: "addition",
            color: "#397535",
          },
          text: "Addition",
        },
        {
          // value: "subtraction",
          value: {
            text: "subtraction",
            color: "#741414",
          },
          text: "Subtraction",
        },
        {
          // value: "multiplication",
          value: {
            text: "multiplication",
            color: "#354675",
          },
          text: "Multiplication",
        },
        {
          // value: "division",
          value: {
            text: "division",
            color: "#c3630a",
          },
          text: "Division",
        },
        {
          // value: "modulo",
          value: {
            text: "modulo",
            color: "#c3630a",
          },
          text: "Modulo (Remainder)",
        },
      ],
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      // shows the result when this is true
      this.form.show = true;
      // evaluates num1 and num2 to the selected operation
      eval(`this.${this.form.operation.text}()`);
      // this object will send all the acquired data from the form...
      let finalData = {
        num1: this.form.num1,
        num2: this.form.num2,
        result: this.form.result,
        operation: this.form.operation.text,
        color: this.form.operation.color,
        show: this.form.show,
      };
      // ...and sends it to the Result.vue via the Home.vue
      this.$emit("sendData", finalData);
    },
    onReset(event) {
      event.preventDefault();
      // this clears the output by sending null values to Result.vue
      let finalData = {
        num1: null,
        num2: null,
        result: null,
        operation: null,
        color: null,
        show: false,
      };
      // this clears the input data from the form
      this.form.num1 = 0;
      this.form.num2 = 0;
      this.form.operation = null;
      this.form.result = null;
      // sends null data to Result.vue via Home.vue
      this.$emit("resetData", finalData);
    },
    // Arithmetic Operations
    addition() {
      this.form.result = parseInt(this.form.num1) + parseInt(this.form.num2);
    },
    subtraction() {
      this.form.result = parseInt(this.form.num1) - parseInt(this.form.num2);
    },
    multiplication() {
      this.form.result = parseInt(this.form.num1) * parseInt(this.form.num2);
    },
    division() {
      this.form.result = parseInt(this.form.num1) / parseInt(this.form.num2);
    },
    modulo() {
      this.form.result = parseInt(this.form.num1) % parseInt(this.form.num2);
    },
  },
};
</script>

<style scoped>
/* Button separation */
.btn {
  margin-right: 10px;
}
</style>
