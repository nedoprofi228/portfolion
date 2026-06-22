<script setup lang="ts">
import { computed } from 'vue'

type Page = 'home' | 'projects' | 'quests' | 'profile' | 'project' | 'quest'

const props = defineProps<{
  page: Page
}>()

const emit = defineEmits<{
  (e: 'navigate', page: Page): void
}>()

const TABS: { label: string; page: Page }[] = [
  { label: 'Главная', page: 'home' },
  { label: 'Проекты', page: 'projects' },
  { label: 'Квесты', page: 'quests' },
  { label: 'Профиль', page: 'profile' },
]

const activePage = computed(() => {
  return TABS.some(t => t.page === props.page) ? props.page : 'projects'
})
</script>

<template>
  <header class="fixed top-0 left-0 right-0 z-50 bg-[#0d1117] border-b border-[#d5d5d5]/20 h-16 select-none">
    <div class="max-w-[1440px] mx-auto px-10 h-full flex items-center justify-between">
      <!-- Logo -->
      <button
        @click="emit('navigate', 'home')"
        class="flex items-center gap-2.5 cursor-pointer hover:opacity-80 transition-opacity duration-150"
      >
        <svg width="28" height="36" viewBox="0 0 28 36" fill="none">
          <path d="M2 3L14 18L2 33" stroke="#D5D5D5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
        </svg>
        <span class="text-[#d5d5d5] text-xl font-normal" :style="{ fontFamily: `'Intel One Mono', 'JetBrains Mono', monospace` }">PortFolion_</span>
      </button>

      <!-- Nav -->
      <nav class="flex items-center gap-10">
        <button
          v-for="tab in TABS"
          :key="tab.page"
          @click="emit('navigate', tab.page)"
          class="relative pb-1 text-[#cfcfcf] text-lg transition-colors hover:text-[#d5d5d5] cursor-pointer"
          :style="{
            fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`,
            opacity: activePage === tab.page ? 1 : 0.76
          }"
        >
          {{ tab.label }}
          <Transition name="slide-up">
            <div
              v-if="activePage === tab.page"
              class="absolute -bottom-[21px] inset-x-0 h-1 rounded-full bg-[#633dff]"
            />
          </Transition>
        </button>
      </nav>

      <!-- User -->
      <div class="flex items-center gap-3">
        <span class="text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Имя пользователя</span>
        <button
          @click="emit('navigate', 'profile')"
          class="w-11 h-11 rounded-xl bg-[#d9d9d9] overflow-hidden flex items-center justify-center cursor-pointer hover:scale-105 transition-transform duration-150"
        >
          <svg width="22" height="22" viewBox="0 0 34 34" fill="none" stroke="#333" stroke-width="2.5" stroke-linecap="round">
            <circle cx="17" cy="11" r="5" />
            <path d="M5 30c0-6 5.4-10 12-10s12 4 12 10" />
          </svg>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}
.slide-up-enter-from,
.slide-up-leave-to {
  opacity: 0;
  transform: translateY(4px) scaleX(0.6);
}
</style>
