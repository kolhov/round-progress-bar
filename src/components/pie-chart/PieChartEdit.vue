<script setup lang="ts">
import type {ChartData} from "chart.js";
import {ChromePicker} from 'vue-color';
import {ref, watch} from "vue";

const chartData = defineModel<ChartData<"pie", number[], unknown>>();
const prop = defineProps<{
  index: number | undefined;
}>();
const emit = defineEmits(['close']);

const newLabel = ref<string>('');
const newValue = ref<number>();
const newColor = ref<string>('#68CCCA');

function save(){
  if (prop.index !== undefined){
    chartData.value.labels[prop.index] = newLabel.value;
    chartData.value.datasets[0].data[prop.index] = newValue.value;
    chartData.value.datasets[0].backgroundColor[prop.index] = newColor.value;
  } else {
    chartData.value = {
      labels: [...chartData.value.labels, newLabel.value],
      datasets: [{
        ...chartData.value.datasets[0],
        data: [...chartData.value.datasets[0].data, newValue.value],
        backgroundColor: [...chartData.value.datasets[0].backgroundColor, newColor.value]
      }]
    };
  }
  emit('close');
}

watch(() => prop.index, (newVal) => {
  if (newVal !== undefined) {
    newLabel.value = chartData.value.labels[newVal];
    newValue.value = chartData.value.datasets[0].data[newVal];
    newColor.value = chartData.value.datasets[0].backgroundColor[newVal];
  }
}, { immediate : true })
</script>

<template>
<div class="flex flex-col gap-4 min-w-80">
  <h2 class="font-semibold">Добавление сектора</h2>
  <div class="relative">
    <input
        v-model="newLabel"
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
        v-model="newValue"
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
      <ChromePicker v-model="newColor" disable-alpha />
    </div>
  </div>
  <button class="addButton" @click="save">
    {{index !== undefined ? 'Обновить сектор' : 'Добавить сектор'}}
  </button>
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

.addButton {
  @apply p-2.5 rounded-md bg-blue-600 w-full text-white hover:bg-blue-500 hover:cursor-pointer;
}

</style>