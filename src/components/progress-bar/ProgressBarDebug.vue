<script setup lang="ts">
import type {ProgressBarState} from "@/components/progress-bar/progress.types.ts";
import {ref} from "vue";

const barState = defineModel<ProgressBarState>('barState');
const percentage = defineModel<number>('percentage');
const dashboard = defineModel<boolean>('dashboard');
const disable = ref<boolean>(false);

function disableButtons(ms: number){
  disable.value = true;
  setTimeout(() => {
    disable.value = false;
  }, ms);
}

function zeroToSuccess(){
  percentage.value = 0;
  barState.value = 'inProgress';
  disableButtons(2550);

  setTimeout(() => {
    percentage.value = 100;
  }, 1500);
  setTimeout(() => {
    barState.value = 'success';
  }, 2500);
}

function zeroToSuccessWithBreakPoints(){
  percentage.value = 0;
  barState.value = 'inProgress';
  disableButtons(5550);

  setTimeout(() => {
    percentage.value = 20;
  }, 1500);
  setTimeout(() => {
    percentage.value = 60;
  }, 2500);
  setTimeout(() => {
    percentage.value = 85;
  }, 3500);
  setTimeout(() => {
    percentage.value = 100;
  }, 4500);
  setTimeout(() => {
    barState.value = 'success';
  }, 5500);
}

function zeroToWarningWithError(){
  percentage.value = 0;
  barState.value = 'inProgress';
  disableButtons(3550);

  setTimeout(() => {
    percentage.value = 30;
  }, 1500);
  setTimeout(() => {
    barState.value = 'warning';
  }, 2500);
  setTimeout(() => {
    barState.value = 'error';
  }, 3500);
}
</script>

<template>
  <div class="flex flex-col">
    <div class="grid grid-cols-2 grid-rows-2 gap-2 max-h-25 justify-center items-center">
      <button class="stateButton" @click="barState = 'warning'">Warning</button>
      <button class="stateButton" @click="barState = 'error'">Error</button>
      <button class="stateButton" @click="barState = 'success'">Success</button>
      <button class="stateButton" @click="barState = 'inProgress'">In progress</button>
    </div>
    <div class="mt-4 w-full flex">
      <label class="p-2 stateButton w-full">
        <input type="checkbox" v-model="dashboard" :disabled="disable"/>
        Dashboard
      </label>
    </div>
    <div class="mt-4 w-full flex">
      <label class="p-2 stateButton w-full">
        <input type="range" v-model="percentage" :disabled="disable"/>
        Percentage
      </label>
    </div>
    <div class="mt-4 w-full flex">
      <button class="stateButton"
              @click="zeroToSuccess"
              :disabled="disable"
      >
        Scenario: zero to success
      </button>
    </div>
    <div class="mt-4 w-full flex">
      <button class="stateButton"
              @click="zeroToSuccessWithBreakPoints"
              :disabled="disable"
      >
        Scenario: zero to success(Breakpoints)
      </button>
    </div>
    <div class="mt-4 w-full flex">
      <button class="stateButton"
              @click="zeroToWarningWithError"
              :disabled="disable"
      >
        Scenario: zero to warning with error
      </button>
    </div>
  </div>
</template>

<style scoped>
@reference "tailwindcss";

.stateButton {
  @apply p-2 text-center rounded-md bg-blue-600 w-full text-white hover:bg-blue-500 hover:cursor-pointer
  disabled:bg-gray-400 disabled:hover:cursor-default;
}
</style>