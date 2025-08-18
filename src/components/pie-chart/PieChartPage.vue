<script setup lang="ts">
import PieChartPanel from "@/components/pie-chart/PieChartPanel.vue";
import PieChart from "@/components/pie-chart/PieChart.vue";

const chartData = {
  labels: ['Красный', 'Синий', 'Жёлтый'],
  datasets: [
    {
      backgroundColor: ['#f87171', '#60a5fa', '#facc15'],
      data: [40, 20, 12]
    }
  ]
};
</script>

<template>
  <PieChartPanel :chart-data="chartData" />
  <PieChart :chart-data="chartData" />
</template>

<style scoped>

</style>