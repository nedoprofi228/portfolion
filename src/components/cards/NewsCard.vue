<script setup lang="ts">
import Tag from '@/components/common/Tag.vue'
import IconComment from '@/components/icons/IconComment.vue'

interface NewsItem {
  id: number
  title: string
  text: string
  comments: string
  border: string
  tags?: readonly (readonly [string, string])[]
}

defineProps<{
  item: NewsItem
}>()
</script>

<template>
  <div
    class="relative rounded-2xl p-5 cursor-pointer news-card transition-all duration-300 hover:-translate-y-0.5"
    :style="{
      background: '#0d1117',
      border: '1px solid #a4a4a4',
      boxShadow: `inset 0 0 0 1px ${item.border}55`,
      '--hover-shadow': `0 0 20px ${item.border}33`
    }"
  >
    <div class="absolute inset-[1px] rounded-2xl pointer-events-none" :style="{ border: `1px solid ${item.border}55` }" />
    <div class="flex items-start gap-2 mb-2">
      <span class="text-[#d5d5d5]/50 text-xl mt-0.5" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">›</span>
      <h3 class="text-[#d5d5d5] text-2xl font-normal flex-1" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ item.title }}</h3>
      <div v-if="item.tags" class="flex gap-1.5 ml-2 flex-wrap justify-end">
        <Tag v-for="tag in item.tags" :key="tag[0]" :label="tag[0]" :color="tag[1]" />
      </div>
    </div>
    <p class="text-[#d5d5d5] text-base leading-relaxed pl-5" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ item.text }}</p>
    <div class="flex items-center justify-end mt-3 gap-4 pl-5">
      <div class="flex items-center gap-1.5 text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
        <IconComment />
        <span>{{ item.comments }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.news-card:hover {
  box-shadow: var(--hover-shadow) !important;
}
</style>
