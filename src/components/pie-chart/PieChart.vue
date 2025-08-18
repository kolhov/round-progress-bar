<script setup lang="ts">
import {Pie} from 'vue-chartjs';
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement
} from 'chart.js';
import type {ChartData} from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, ArcElement);

defineProps<{
  chartData: ChartData<"pie", number[], unknown>
}>();

const chartOptions = {
  responsive: true,
};

</script>

<template>
  <Pie
      id="pie-chart"
      :options="chartOptions"
      :data="chartData"
  />
</template>

<style scoped>

</style>