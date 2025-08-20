<script setup lang="ts">
import {shallowRef} from "vue";
import PieChartPage from '@/components/pie-chart/PieChartPage.vue';
import ProgressBarPage from '@/components/progress-bar/ProgressBarPage.vue';

const page = shallowRef(PieChartPage);

const selectPage = (x: EPages) => {
  if (x == EPages.PROGRESS_BAR) {
    page.value = ProgressBarPage;
  }
  if (x == EPages.PIE_CHART) {
    page.value = PieChartPage;
  }
}

enum EPages {
  PROGRESS_BAR,
  PIE_CHART
}
</script>

<template>
  <div class="flex flex-col justify-center items-center gap-6 mt-6">
    <div class="bg-gray-200 rounded-sm">
      <button @click="selectPage(EPages.PROGRESS_BAR)">Progress bar</button>
      <button @click="selectPage(EPages.PIE_CHART)">Pie chart</button>
    </div>
    <component class="w-full max-w-240 h-120 justify-between" :is="page"/>
  </div>
</template>

<style scoped>
@reference "tailwindcss";

button {
  @apply p-1.5 px-4 rounded-md m-2 bg-blue-600 text-white hover:bg-blue-500 hover:cursor-pointer
}
</style>
