<script setup lang="ts">
withDefaults(defineProps<{
  src?: string
  size?: number
}>(), {
  size: 44
})
</script>

<template>
  <div
    class="rounded-xl bg-[#d9d9d9] flex-shrink-0 overflow-hidden"
    :style="{ width: size + 'px', height: size + 'px' }"
  >
    <img v-if="src" :src="src" alt="" class="w-full h-full object-cover" />
  </div>
</template>
