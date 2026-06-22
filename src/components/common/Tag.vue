<script setup lang="ts">
defineProps<{
  label: string
  color: string
}>()
</script>

<template>
  <span
    class="px-2 py-0.5 rounded text-sm leading-none"
    :style="{
      fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`,
      color: color,
      border: '1px solid currentColor',
      opacity: 0.9
    }"
  >
    {{ label }}
  </span>
</template>
