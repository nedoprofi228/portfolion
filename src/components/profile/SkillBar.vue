<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<{
  lang: string
  color: string
  level: string
  level_n: number
}>()

const LEVEL_COLORS: Record<string, string> = { 
  Junior: '#0e7600', 
  Middle: '#e88700', 
  Senior: '#642dd3' 
}

const bars = [1, 2, 3, 4]
const animated = ref(false)

onMounted(() => {
  setTimeout(() => {
    animated.value = true
  }, 50)
})
</script>

<template>
  <div>
    <div class="flex items-center justify-between mb-1.5">
      <span class="text-2xl font-normal" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, color: color }">{{ lang }}</span>
      <span class="text-xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, color: LEVEL_COLORS[level] }">{{ level }}</span>
    </div>
    <div class="flex gap-1.5">
      <div
        v-for="b in bars"
        :key="b"
        class="flex-1 h-2 rounded-full origin-left transition-transform duration-400"
        :style="{
          background: b <= level_n ? '#ff9809' : 'white',
          transform: animated ? 'scaleX(1)' : 'scaleX(0)',
          transitionDelay: `${b * 80}ms`
        }"
      />
    </div>
    <div class="h-px bg-white/20 mt-3" />
  </div>
</template>
