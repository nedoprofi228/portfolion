<script setup lang="ts">
import SearchBar from '@/components/common/SearchBar.vue'
import QuestCard from '@/components/cards/QuestCard.vue'

type Page = 'home' | 'projects' | 'quests' | 'profile' | 'project' | 'quest'

const emit = defineEmits<{
  (e: 'navigate', page: Page): void
}>()

const QUESTS = [
  { id: 1, title: 'Создайте консольный чат_', desc: 'Вам необходимо создать консольное приложение которое предоставляет доступ к возможности общения с помощью протоколов udp или tcp.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#ff9809', done: false },
  { id: 2, title: 'Создайте 10 проектов_', desc: 'Вам необходимо создать 10 любых проектов, которые соответствуют минимальным требованиями: 10к строк, 10 файлов, структура.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#3cb4ff', done: false },
  { id: 3, title: 'Создайте 10 проектов_', desc: 'Вам необходимо создать 10 любых проектов, которые соответствуют минимальным требованиями: 10к строк, 10 файлов, структура.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#ff9809', done: true },
  { id: 4, title: 'Создайте 10 проектов_', desc: 'Вам необходимо создать 10 любых проектов, которые соответствуют минимальным требованиями: 10к строк, 10 файлов, структура.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#25ed13', done: true },
  { id: 5, title: 'Создайте 10 проектов_', desc: 'Вам необходимо создать 10 любых проектов, которые соответствуют минимальным требованиями: 10к строк, 10 файлов, структура.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#25ed13', done: true },
]
</script>

<template>
  <div class="max-w-[1440px] mx-auto px-10 py-10">
    <SearchBar />
    <div class="grid grid-cols-2 gap-6">
      <QuestCard
        v-for="(q, i) in QUESTS"
        :key="q.id"
        :q="q"
        @click="emit('navigate', 'quest')"
        class="quest-item-fade"
        :style="{ animationDelay: `${i * 70}ms` }"
      />
    </div>
  </div>
</template>

<style scoped>
.quest-item-fade {
  animation: scaleIn 0.35s ease-out both;
}

@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.95);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
