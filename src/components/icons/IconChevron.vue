<script setup lang="ts">
defineProps<{
  dir?: 'left' | 'right'
}>()
</script>

<template>
  <svg width="10" height="18" viewBox="0 0 10 18" fill="none" stroke="#d5d5d5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
    :style="{ transform: dir === 'left' ? 'scaleX(-1)' : undefined }">
    <path d="M2 2l6 7-6 7" />
  </svg>
</template>
