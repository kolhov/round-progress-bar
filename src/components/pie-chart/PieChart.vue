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
import {computed, watch} from "vue";

ChartJS.register(Title, Tooltip, Legend, ArcElement);

const props = defineProps<{
  chartData: ChartData<"pie", number[], unknown>
}>();

const chartOptions = {
  responsive: true,
};

const chartKey = computed(() =>
    JSON.stringify(props.chartData.datasets.map(d => d.data)).slice(0, 50)
);
</script>

<template>
  <div class="chart-wrapper">
    <div class="chart-container">
      <Pie
          id="pie-chart"
          :key="chartKey"
          :options="chartOptions"
          :data="chartData"
      />
    </div>
  </div>
</template>

<style scoped>
.chart-wrapper {
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
}

.chart-container {
  position: relative;
  width: 100%;
  padding-bottom: 100%; /* Создает квадратный контейнер */
  height: 0;
}

.chart-container > * {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>