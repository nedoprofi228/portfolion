<script setup lang="ts">
import Tag from '@/components/common/Tag.vue'
import IconHeart from '@/components/icons/IconHeart.vue'
import IconFork from '@/components/icons/IconFork.vue'
import IconShare from '@/components/icons/IconShare.vue'

interface ProjectItem {
  id: number
  title: string
  description: string
  tags: readonly (readonly [string, string])[]
  reactions: readonly string[]
}

defineProps<{
  p: ProjectItem
}>()

const emit = defineEmits<{
  (e: 'click'): void
}>()
</script>

<template>
  <div
    @click="emit('click')"
    class="bg-[#0d1117] border border-[#a4a4a4] rounded-2xl p-5 cursor-pointer hover:-translate-y-0.5 hover:border-[#d5d5d5]/50 transition-all duration-150"
  >
    <div class="flex items-start justify-between gap-4 mb-2">
      <div class="flex items-center gap-2">
        <span class="text-[#d5d5d5]/60 text-2xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">›</span>
        <h3 class="text-[#d5d5d5] text-2xl font-normal" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ p.title }}</h3>
      </div>
      <div class="flex gap-1.5 flex-shrink-0 pt-1">
        <Tag v-for="tag in p.tags" :key="tag[0]" :label="tag[0]" :color="tag[1]" />
      </div>
    </div>
    <p class="text-[#d5d5d5] text-lg leading-relaxed pl-6 mb-4" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ p.description }}</p>
    <div class="flex items-center justify-between pl-6">
      <span
        class="text-[#78beff] text-lg cursor-pointer hover:underline hover:translate-x-1 transition-transform duration-150 inline-block"
        :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
      >
        подробнее...
      </span>
      
      <!-- Reactions -->
      <div class="flex items-center gap-5" @click.stop>
        <button class="flex items-center gap-1.5 text-[#d5d5d5] hover:text-white cursor-pointer hover:scale-110 active:scale-95 transition-all duration-150">
          <IconHeart red />
          <span class="text-base" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ p.reactions[0] }}</span>
        </button>
        <button class="flex items-center gap-1.5 text-[#d5d5d5] hover:text-white cursor-pointer hover:scale-110 active:scale-95 transition-all duration-150">
          <IconFork />
          <span class="text-base" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ p.reactions[1] }}</span>
        </button>
        <button class="flex items-center gap-1.5 text-[#d5d5d5] hover:text-white cursor-pointer hover:scale-110 active:scale-95 transition-all duration-150">
          <IconShare />
          <span class="text-base" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ p.reactions[2] }}</span>
        </button>
      </div>
    </div>
  </div>
</template>
