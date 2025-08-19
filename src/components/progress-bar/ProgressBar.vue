<script setup lang="ts">
import type {ProgressBarState} from "@/components/progress-bar/progress.bar.types.ts";
import {computed, onMounted, ref} from "vue";

const WARNING_COLOR = '#1cff37'
const ERROR_COLOR = '#fc0f1f'
const INIT_COLOR = '#f7022f'
const MIDDLE_COLOR = '#7045ff'
const FINISH_COLOR = '#439423'

const percentage = ref<number>(0);
const color = ref<string>(INIT_COLOR);
const state = ref<ProgressBarState>('inProgress');

const CIRCUMFERENCE = 375; // calculated 2 * Math.PI * circle radius
const strokeOffset = ref<number>(CIRCUMFERENCE);

const props = defineProps<{
  dashboard?: boolean
}>()

function setProgress(newPercentage: number) {
  const clamped = Math.min(newPercentage, 100);
  let offset;
  if (props.dashboard) {
    offset = CIRCUMFERENCE - CIRCUMFERENCE * (clamped / 100) + clamped;
  } else {
    offset = CIRCUMFERENCE - CIRCUMFERENCE * (clamped / 100);
  }
  strokeOffset.value = offset;

  if (clamped >= 25 && percentage.value <= 75) {
    color.value = MIDDLE_COLOR;
  }

  if (clamped > 75) {
    setTimeout(() => {
      color.value = FINISH_COLOR;
    }, 500);
  }

  if (clamped == 100) {
    setTimeout(() => {
      state.value = 'success';
    }, 1000);
  }

  percentage.value = clamped;
}

function setBarState(newState: ProgressBarState) {
  state.value = newState;

  if (newState == 'error') {
    color.value = ERROR_COLOR;
  } else if (newState == 'warning') {
    color.value = WARNING_COLOR;
  }
}

onMounted(() => {
  setTimeout(() => {
    setProgress(25);
    // setTimeout(() => {
    //   setBarState('error');
    // }, 700)
    // setTimeout(() => {
    //   setBarState('warning');
    // }, 1400)
  }, 400)
  setTimeout(() => {
    setProgress(50);
  }, 2000)
  setTimeout(() => {
    setProgress(100);
  }, 3000)
})
</script>

<template>
  <svg xmlns="http://www.w3.org/2000/svg"
       viewBox="0 0 160 160"
  >
    <circle
        v-if="!dashboard"
        fill="none" opacity=".2"
        stroke="#FF156D" stroke-width="10"
        stroke-linecap="round"
        cx="80" cy="80" r="60"/>
    <circle

        class="bar"
        :transform="!dashboard ? 'rotate(270)' : 'rotate(140)'"
        transform-origin="center"
        cx="80" cy="80" r="60"
        fill="none"
        :stroke="color"
        stroke-width="10"
        stroke-linecap="round"
        :stroke-dasharray="CIRCUMFERENCE"
        :stroke-dashoffset="strokeOffset"
    />
    <circle
        v-if="dashboard"
        class="bar"
        opacity=".2"
        transform="rotate(140)"
        transform-origin="center"
        cx="80" cy="80" r="60"
        fill="none"
        stroke="#FF156D"
        stroke-width="10"
        stroke-linecap="round"
        stroke-dasharray="320"
        stroke-dashoffset="45"
    />
    <!--    <circle-->
    <!--        v-if="dashboard"-->
    <!--        class="bar"-->
    <!--        transform="rotate(140)"-->
    <!--        transform-origin="center"-->
    <!--        cx="80" cy="80" r="60"-->
    <!--        fill="none"-->
    <!--        :stroke="color"-->
    <!--        stroke-width="10"-->
    <!--        stroke-linecap="round"-->
    <!--        stroke-dasharray="375"-->
    <!--        :stroke-dashoffset="strokeOffset"-->
    <!--    />-->
    <text v-if="state == 'inProgress'"
          text-anchor="middle"
          x="50%"
          y="50%"
          dy=".3em"
          font-family="Roboto, Arial, sans-serif"
          fill="#6E6E6E"
    >
      {{ percentage }}%
    </text>
    <path v-else-if="state == 'success'"
          fill="none"
          :stroke="color" stroke-linecap="round" stroke-linejoin="round"
          stroke-width="2"
          transform="translate(70, 68)"
          d="M20 6L9 17l-5-5"
    />
    <path v-else-if="state == 'warning'"
          :fill="WARNING_COLOR"
          transform="translate(70, 68) scale(0.7)"
          d="M16 2C8.3 2 2 8.3 2 16s6.3 14 14 14s14-6.3 14-14S23.7 2 16 2m-1.1 6h2.2v11h-2.2zM16 25c-.8 0-1.5-.7-1.5-1.5S15.2 22 16 22s1.5.7 1.5 1.5S16.8 25 16 25"
    />
    <path v-else-if="state == 'error'"
          :fill="ERROR_COLOR" fill-rule="evenodd"
          stroke="#f7f4f4" stroke-linecap="round" stroke-linejoin="round" stroke-width="0"
          d="m6 11l5-5l13 13L37 6l5 5l-13 13l13 13l-5 5l-13-13l-13 13l-5-5l13-13z"
          transform="translate(70, 68) scale(0.5)"
          clip-rule="evenodd"
    />
  </svg>
</template>

<style scoped>
.bar {
  transition: stroke-dashoffset 1s ease, stroke 1s ease;
}
</style>