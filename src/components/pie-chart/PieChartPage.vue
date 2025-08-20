<script setup lang="ts">
import PieChartPanel from "@/components/pie-chart/PieChartPanel.vue";
import PieChart from "@/components/pie-chart/PieChart.vue";
import {ref} from "vue";

const chartData = ref({
  labels: ['Красный', 'Синий', 'Жёлтый', 'Жё'],
  datasets: [
    {
      backgroundColor: ['#f87171', '#60a5fa', '#facc15', '#fa1115'],
      data: [40, 20, 3, 3]
    }
  ]
});

</script>

<template>
  <div>
    <div class="mb-8">
      <h1 class="text-xl pb-2">Круговая диаграмма</h1>
      <hr />
    </div>
    <div class="flex flex-row">
      <PieChartPanel v-model:chart-data="chartData" />
      <PieChart :chart-data="chartData" />
    </div>
  </div>
</template>

<style scoped>

</style>