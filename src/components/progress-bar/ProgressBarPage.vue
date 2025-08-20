<script setup lang="ts">
import ProgressBar from './ProgressBar.vue'
import ProgressBarDebug from './ProgressBarDebug.vue'
import {ref} from "vue";
import type {ProgressBarState} from "@/components/progress-bar/progress.types.ts";

const percentage = ref<number>(20);
const barState = ref<ProgressBarState>('inProgress');

</script>

<template>
  <div>
    <ProgressBarDebug />
    <ProgressBar :percentage="percentage" :state="barState"/>
  </div>
</template>

<style scoped>

</style>