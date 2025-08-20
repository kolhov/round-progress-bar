<script setup lang="ts">
import ProgressBar from './ProgressBar.vue'
import ProgressBarDebug from './ProgressBarDebug.vue'
import {ref} from "vue";
import type {ProgressBarState} from "@/components/progress-bar/progress.types.ts";

const percentage = ref<number>(20);
const barState = ref<ProgressBarState>('inProgress');
const dashboard = ref<boolean>(false);

</script>

<template>
  <div>
    <div class="mb-8">
      <h1 class="text-xl pb-2">Progress bar</h1>
      <hr />
    </div>
    <div class="flex justify-center">
      <ProgressBarDebug
          class="min-w-80 mr-8"
          v-model:percentage="percentage"
          v-model:bar-state="barState"
          v-model:dashboard="dashboard"
      />
      <ProgressBar
          :percentage="percentage"
          :state="barState"
          class="max-w-70"
          :dashboard="dashboard"
      />
    </div>
  </div>
</template>

<style scoped>

</style>