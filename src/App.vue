<script setup lang="ts">
import { shallowRef } from "vue";
import PieChartPage from '@/components/pie-chart/PieChartPage.vue';
import ProgressBarPage from '@/components/progress-bar/ProgressBarPage.vue';

const page = shallowRef(PieChartPage);

const selectPage = (x: EPages) => {
  if (x == EPages.PROGRESS_BAR){
    page.value = ProgressBarPage;
  }
  if (x == EPages.PIE_CHART){
    page.value = PieChartPage;
  }
}

enum EPages {
  PROGRESS_BAR,
  PIE_CHART
}
</script>

<template>
<!--селектор странички-->
  <button @click="selectPage(EPages.PROGRESS_BAR)">Progress bar</button>
  <button @click="selectPage(EPages.PIE_CHART)">Pie chart</button>
<!--страничка-->
  <component :is="page" />
</template>

<style scoped></style>
