<script setup lang="ts">
defineProps<{
  red?: boolean
}>()
</script>

<template>
  <svg width="22" height="22" viewBox="0 0 34 34" fill="none" :stroke="red ? '#E00505' : '#d5d5d5'" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
    <path d="M17 29S4 21 4 12a7 7 0 0 1 13-3.5A7 7 0 0 1 30 12c0 9-13 17-13 17z" />
  </svg>
</template>
