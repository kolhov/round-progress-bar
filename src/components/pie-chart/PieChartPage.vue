<script setup lang="ts">
import PieChartPanel from "@/components/pie-chart/PieChartPanel.vue";
import PieChart from "@/components/pie-chart/PieChart.vue";
import {ref} from "vue";

const chartData = ref({
  labels: ['Красный', 'Синий', 'Жёлтый'],
  datasets: [
    {
      backgroundColor: ['#f87171', '#60a5fa', '#facc15'],
      data: [40, 20, 3]
    }
  ]
});

</script>

<template>
  <div>
    <PieChartPanel v-model:chart-data="chartData" />
    <PieChart :chart-data="chartData" />
  </div>
</template>

<style scoped>

</style>