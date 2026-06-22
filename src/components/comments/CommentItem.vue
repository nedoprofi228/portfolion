<script setup lang="ts">
import { ref } from 'vue'
import Avatar from '@/components/common/Avatar.vue'

interface Comment {
  author: string
  role: string
  roleColor: string
  time: string
  text: string
  replies?: Comment[]
}

defineProps<{
  c: Comment
  depth?: number
}>()

const open = ref(true)
</script>

<template>
  <div :class="depth && depth > 0 ? 'border-l border-white/20 pl-6 mt-4' : 'mt-6'">
    <div class="flex items-start gap-3">
      <Avatar :size="40" />
      <div class="flex-1">
        <div class="flex items-center gap-2 flex-wrap">
          <span class="text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ c.author }}</span>
          <span class="text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, color: c.roleColor }">{{ c.role }}</span>
          <span class="text-[#d5d5d5]/50 text-xs ml-auto" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ c.time }}</span>
        </div>
        <p class="text-[#d5d5d5] text-xl mt-1 leading-snug" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ c.text }}</p>
        <button
          v-if="c.replies && c.replies.length > 0"
          @click="open = !open"
          class="text-[#d5d5d5]/50 text-xs mt-1 hover:text-[#d5d5d5] transition-colors cursor-pointer"
          :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
        >
          {{ open ? 'скрыть ответы' : `показать ${c.replies.length} ответа` }}
        </button>
      </div>
    </div>
    <div v-if="open && c.replies && c.replies.length > 0">
      <!-- Recursive reference to CommentItem -->
      <CommentItem
        v-for="(r, i) in c.replies"
        :key="i"
        :c="r"
        :depth="(depth || 0) + 1"
      />
    </div>
  </div>
</template>
