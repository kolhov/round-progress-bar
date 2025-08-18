<script setup lang="ts">

</script>

<template>
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200">
    <radialGradient id="a12">
      <stop stop-color="#FF156D"/>
    </radialGradient>
    <circle
        transform="rotate(270)"
        transform-origin="center"
        cx="100" cy="100" r="70"
        fill="none"
        stroke="url(#a12)"
        stroke-width="15"
        stroke-linecap="round"
        stroke-dasharray="439"
        stroke-dashoffset="439"
    >
      <animate
          attributeName="stroke-dashoffset"
          from="440" to="0"
          dur="2s"
          fill="freeze" />
    </circle>
    <circle fill="none" opacity=".2" stroke="#FF156D" stroke-width="15" stroke-linecap="round" cx="100" cy="100" r="70"/>
  </svg>

</template>

<style scoped>

</style>