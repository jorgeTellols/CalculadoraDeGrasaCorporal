<script>
import WBodyFatCalculator from "../widgets/w-body-fat-calculator.vue";

export default {
  components: {
    WBodyFatCalculator,
  }
}
</script>

<template>
  <div class="flex flex-col justify-center items-center h-screen text-2xl py-20">
    <div class="title-container">
      <h1 class="font-medium">Calcular grasa corporal</h1>
    </div>
    <div class=" body-fat-calculator-container mt-10">
      <WBodyFatCalculator />
    </div>
  </div>
</template>

<style>
html {
  background-image: linear-gradient(135deg, #66cccc, #99ff99);
}
</style>
