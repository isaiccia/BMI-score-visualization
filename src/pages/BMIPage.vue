<template>
  <div>
    <div
      class="container border col-md-6 p-3 mt-5 shadow p-3 mb-5 bg-body rounded"
    >
      <h2 class="text-center my-3">Welcome to your pet's BMI Calculator</h2>
      <form @submit="calculateBmi" class="mb-4">
        <div class="mb-3">
          <label>Weight in kg </label>
          <input
            class="form-control"
            type="number"
            v-model="mass"
            :placeholder="mass"
          />
        </div>
        <div class="mb-3">
          <label>Height in cm </label>
          <input
            class="form-control"
            type="number"
            v-model="height"
            :placeholder="height"
          />
        </div>

        <button
          class="calculate btn btn-outline-primary"
          @click.prevent="calculateBmi"
        >
          Calculate
        </button>
      </form>
      <h5>{{ result }}</h5>
    </div>
    <BMIVisualizer
      v-if="isShown"
      :activeColor="activeColor"
      :bmi="bmi"
      :message="message"
    ></BMIVisualizer>
  </div>
</template>

<script>
import BMIVisualizer from "../components/BMIVisualizer.vue";

export default {
  components: { BMIVisualizer },
  name: "BmiCalculator",

  data() {
    return {
      mass: "kg",
      height: "cm",
      result: "",
      activeColor: "",
      bmi: "",
      isShown: "",
      message: "",
    };
  },
  methods: {
    calculateBmi() {
      const bmi = +(this.mass / Math.pow(this.height / 100, 2)).toFixed(1);
      if (this.mass === "" || this.height === "") {
        alert("Inputs can not be empty");
      } else if (this.mass <= 0 || this.height <= 0) {
        alert("Inputs can not be negative");
      }
      if (bmi < 30 && bmi > 0) {
        this.isShown = true;
        this.activeColor = "#F49C94";
        this.bmi = `${bmi}`;
        this.result = `Your pet's bmi is ${bmi}. They are underweight 😰`;
        this.message = "Underweight";
      } else if (bmi >= 30 && bmi < 90) {
        this.isShown = true;
        this.bmi = `${bmi}`;
        this.activeColor = "#9CED73";
        this.result = `Your pet's bmi is ${bmi}. Their weight is normal 🐶🐱`;
        this.message = "Normal Weight";
      } else if (bmi >= 90 && bmi <= 120) {
        this.isShown = true;
        this.bmi = `${bmi}`;
        this.activeColor = "#F03C08";
        this.result = `Your pet's bmi is ${bmi}. They are overweight 😥`;
        this.message = "Overweight";
      } else if (bmi < 0 || bmi > 120) {
        this.isShown = false;
        this.result = "The data are invalid";
      }
    },
  },
};
</script>

<style></style>
