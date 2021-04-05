<template>
  <div class="home">
    <div class="container">
      <b-card-group>
        <b-card>
          <Calculator @sendData="getFormData" @resetData="getFormData" />
        </b-card>
        <b-card
          v-show="formData.show"
          :style="{
            backgroundColor: formData.color,
            borderColor: formData.color,
          }"
        >
          <Result :setFormData="formData" />
        </b-card>
      </b-card-group>
    </div>
  </div>
</template>

<script>
import Calculator from "@/components/Calculator.vue";
import Result from "@/components/Result.vue";
export default {
  name: "Home",
  components: {
    Calculator,
    Result,
  },
  data() {
    return {
      formData: {},
    };
  },
  methods: {
    getFormData(formData) {
      this.formData = formData;
    },
  },
};
</script>
