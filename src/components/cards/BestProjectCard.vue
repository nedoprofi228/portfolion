<script setup lang="ts">
import Avatar from '@/components/common/Avatar.vue'
import IconHeart from '@/components/icons/IconHeart.vue'
import IconFork from '@/components/icons/IconFork.vue'
import IconShare from '@/components/icons/IconShare.vue'

import imgAuthorQpro from '@/assets/author-qpro.png'
import imgAuthorLittlecode from '@/assets/author-littlecode.png'

defineProps<{
  title: string
  author: string
  imgs: string[]
  reactions: string[]
}>()

const emit = defineEmits<{
  (e: 'click'): void
}>()
</script>

<template>
  <div
    @click="emit('click')"
    class="bg-[#0d1117] border border-[#9e9898] rounded-2xl p-4 cursor-pointer hover:border-[#d5d5d5]/50 hover:-translate-y-0.5 active:scale-[0.99] transition-all duration-150"
  >
    <div class="flex gap-2 mb-3">
      <div v-if="imgs[0]" class="w-24 h-24 rounded-xl overflow-hidden flex-shrink-0">
        <img :src="imgs[0]" class="w-full h-full object-cover" alt="" />
      </div>
      <div class="flex flex-col gap-1.5">
        <div v-for="(img, i) in imgs.slice(1)" :key="i" class="w-14 h-[44px] rounded-lg overflow-hidden">
          <img :src="img" class="w-full h-full object-cover" alt="" />
        </div>
      </div>
    </div>
    <div class="flex items-center gap-1.5 mb-2">
      <span class="text-[#d5d5d5]/50 text-lg" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">›</span>
      <span class="text-[#d5d5d5] text-lg" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ title }}</span>
    </div>
    <div class="flex items-center gap-2 mb-3">
      <Avatar :src="author === 'Qpro_' ? imgAuthorQpro : imgAuthorLittlecode" :size="36" />
      <span class="text-[#d5d5d5] text-base" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ author }}</span>
    </div>
    <div class="flex items-center gap-4">
      <div v-for="(r, i) in reactions" :key="i" class="flex items-center gap-1 text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
        <IconHeart v-if="i === 0" red />
        <IconFork v-else-if="i === 1" />
        <IconShare v-else />
        <span>{{ r }}</span>
      </div>
    </div>
  </div>
</template>
