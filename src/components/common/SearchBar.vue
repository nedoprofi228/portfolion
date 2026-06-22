<script setup lang="ts">
import { ref } from 'vue'
import IconSearch from '@/components/icons/IconSearch.vue'
import IconFilter from '@/components/icons/IconFilter.vue'

withDefaults(defineProps<{
  placeholder?: string
}>(), {
  placeholder: 'текст поиска_'
})

const val = ref('')
</script>

<template>
  <div class="flex items-center gap-3 mb-8">
    <div class="flex-1 flex items-center gap-3 bg-[#0d1117] border border-[#d5d5d5]/40 rounded-2xl px-4 py-2 hover:border-[#d5d5d5]/70 transition-colors">
      <IconSearch />
      <input
        v-model="val"
        :placeholder="placeholder"
        class="flex-1 bg-transparent text-[#d5d5d5] text-lg outline-none placeholder:text-[#d5d5d5]/40"
        :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
      />
    </div>
    <button class="p-2.5 border border-[#d5d5d5]/40 rounded-xl hover:border-[#d5d5d5]/80 transition-colors hover:scale-108 active:scale-95 transition-transform duration-150">
      <IconFilter />
    </button>
  </div>
</template>
