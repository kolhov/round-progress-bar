<script setup lang="ts">
import type {ChartData} from "chart.js";
import {ChromePicker, SketchPicker} from 'vue-color';
import {ref} from "vue";

const chartData = defineModel<ChartData<"pie", number[], unknown>>('chartData');
const prop = defineProps<{
  index: number
}>();

const newLabel = ref<string>('');
const newValue = ref<number>();
const color = ref<string>('#68CCCA');
</script>

<template>
<div class="flex flex-col gap-4 min-w-80">
  <h2 class="font-semibold">Добавление сектора</h2>
  <div class="relative">
    <input
        v-model="index ? chartData!.labels[index] : newLabel"
        type="text"
        id="input"
        placeholder=" "
        class="formInput peer"
    />
    <label
        for="input"
        class="formLabel"
    >
      Наименование
    </label>
  </div>
  <div class="relative">
    <input
        v-model="value"
        type="text"
        id="input"
        placeholder=" "
        class="formInput peer"
    />
    <label
        for="input"
        class="formLabel"
    >
      Значение
    </label>
    <div class="flex justify-center mt-4">
      <SketchPicker v-model="color" />
    </div>
  </div>
</div>
</template>

<style scoped>
@reference 'tailwindcss';

.formInput {
  @apply w-full border rounded-md px-3 pt-5 pb-2 text-sm
  outline-none border-gray-300 focus:border-blue-500
  focus:ring-1 focus:ring-blue-500;
}

.formLabel {
  @apply absolute left-3 top-2 text-gray-400 text-xs transition-all
  peer-placeholder-shown:top-4 peer-placeholder-shown:text-gray-400 peer-placeholder-shown:text-sm
  peer-focus:top-2 peer-focus:text-xs peer-focus:text-blue-500;
}


</style>