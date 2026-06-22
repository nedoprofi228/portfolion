<script setup lang="ts">
import Tag from '@/components/common/Tag.vue'
import IconDone from '@/components/icons/IconDone.vue'
import IconStar from '@/components/icons/IconStar.vue'
import IconUsers from '@/components/icons/IconUsers.vue'
import { computed } from 'vue'

interface QuestItem {
  id: number
  title: string
  desc: string
  tags: readonly (readonly [string, string])[]
  xp: string
  stars: number
  users: string
  border: string
  done: boolean
}

const props = defineProps<{
  q: QuestItem
}>()

const emit = defineEmits<{
  (e: 'click'): void
}>()

const borderColor = computed(() => {
  return props.q.done ? '#25ed13' : props.q.border
})
</script>

<template>
  <div
    @click="emit('click')"
    class="relative rounded-2xl p-5 cursor-pointer quest-card transition-all duration-300 hover:-translate-y-1"
    :style="{
      background: '#0d1117',
      border: `1px solid ${borderColor}`,
      boxShadow: `inset 0 0 0 1px ${borderColor}30`,
      '--hover-shadow': `0 4px 24px ${borderColor}44`
    }"
  >
    <!-- Second border offset -->
    <div class="absolute inset-[6px] rounded-xl pointer-events-none" style="border: 1px solid rgba(213, 213, 213, 0.15)" />
    
    <div class="absolute top-3 right-3">
      <IconDone v-if="q.done" />
      <div v-else class="w-2.5 h-2.5 rounded-full mt-1 mr-1" :style="{ background: q.border }" />
    </div>

    <!-- Tags top row -->
    <div class="flex gap-1.5 mb-3">
      <Tag v-for="tag in q.tags" :key="tag[0]" :label="tag[0]" :color="tag[1]" />
    </div>

    <!-- Title -->
    <div class="flex items-start gap-2 mb-3">
      <span :style="{ color: q.border, fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, fontSize: '20px' }">›</span>
      <h3 class="text-2xl font-normal leading-tight" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, color: '#ff9809' }">{{ q.title }}</h3>
    </div>

    <p class="text-[#d5d5d5] text-base leading-relaxed mb-5" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ q.desc }}</p>

    <!-- Footer badges -->
    <div class="flex items-center justify-between">
      <div class="flex items-center gap-2">
        <span class="px-2.5 py-1 rounded text-sm font-normal" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, background: '#3f09ac', color: '#25ed13' }">{{ q.xp }}</span>
        <div class="flex items-center gap-1 px-2 py-1 rounded" style="background: #49307c">
          <IconStar />
          <span class="text-[#ff9809] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ q.stars }}</span>
        </div>
      </div>
      <div class="flex items-center gap-1.5 text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
        <IconUsers />
        <span>{{ q.users }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.quest-card:hover {
  box-shadow: var(--hover-shadow) !important;
}
</style>
