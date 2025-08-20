<script setup lang="ts">
import type {ChartData} from "chart.js";
import {Icon} from '@iconify/vue';

const chartData = defineModel<ChartData<"pie", number[], unknown>>('chartData');

function addSector(){

}
function editSector(){

}

function deleteSector(index: number){
  if (!chartData.value) return;

  if (chartData.value?.labels){
    chartData.value.labels = chartData.value?.labels.filter((_, i) => i !== index);
  }

  chartData.value.datasets[0].backgroundColor = (
      (chartData.value.datasets[0].backgroundColor as string[]).filter((_, i) => i !== index)
  )

  chartData.value.datasets[0].data = chartData.value.datasets[0].data.filter((_, i) => i !== index)
}
</script>

<template>
  <div class="flex flex-col gap-y-4">
    <div v-for="(data, index) in chartData?.datasets[0].data"
         :key="`${index}-dataset`"
         class="flex justify-between gap-4 bg-blue-100 p-2.5 rounded-md items-center"
    >
      <div class="flex gap-4">
        <span v-if="chartData?.labels"
              class="min-w-30"
        >
          {{ chartData?.labels[index] }}
        </span>
        <div class="divider"/>
        <span class="min-w-12 text-center">{{ data }}</span>
        <div class="divider"/>
        <div v-if="chartData?.datasets[0].backgroundColor"
              class="w-5 h-5 rounded-full place-self-center mr-8"
              :style="{backgroundColor: (chartData?.datasets[0].backgroundColor as string[])[index]}"
        />
      </div>
      <div>
        <button class="editBut">
          <Icon icon="iconamoon:edit-light"/>
        </button>
        <button class="editBut" @click.prevent="deleteSector(index)">
          <Icon icon="material-symbols:delete-outline"/>
        </button>
      </div>
    </div>
    <button class="addButton ">Добавить сектор</button>
  </div>
</template>

<style scoped>
@reference "tailwindcss";

.addButton {
  @apply p-2.5 rounded-md bg-blue-600 w-full text-white hover:bg-blue-500 hover:cursor-pointer;
}

.editBut {
  @apply p-2 hover:bg-blue-300 hover:cursor-pointer rounded-md;
}

.divider {
  @apply border border-gray-300 rounded;
}
</style>