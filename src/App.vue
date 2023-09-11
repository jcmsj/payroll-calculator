<template>
  <form action="#" class="card flex flex-col items-center">
    <div class="card-title">Payroll Calculator:</div>
    <div class="card-body flex-col justify-center items-center p-4">
      <label for="rate">Hourly rate:</label>
      <input type="number" id="rate" v-model="rate" class="input" />
      <label for="hours">Number of hours worked:</label>
      <input type="number" id="hours" v-model="hours" />
      <label for="">Allowance:</label>
      <input type="number" v-model="allowance">
      <label for="">SSS Contribution:</label>
      <input type="number" v-model="sss">
      <label for="">Philhealth Contribution:</label>
      <input type="number" v-model="philhealth">
      <label for="">Pag-ibig Contribution:</label>
      <input type="number" v-model="pagibig">
    </div>
  </form>
  <br>
  <div class="card card-compact border-primary">
    <div class="card-title">Net Pay:</div>
    <div class="card-body">
      <p>Php {{ netpay }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue';

const hours = ref(0);
const rate = ref(0);
const sss = ref(0);
const allowance = ref(0);
const philhealth = ref(0);
const pagibig = ref(0);
const netpay = computed(() => {
  const additive = allowance.value
  const totalDeductions = sss.value + philhealth.value + pagibig.value;
  const grossPay = hours.value * rate.value;
  return grossPay - totalDeductions + additive;
});
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  width: 100vw;
}

label {
  display: block;
}

input {
  @apply input
}
</style>
