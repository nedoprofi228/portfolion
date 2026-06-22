<script setup lang="ts">
import SearchBar from '@/components/common/SearchBar.vue'
import ProjectCard from '@/components/cards/ProjectCard.vue'

type Page = 'home' | 'projects' | 'quests' | 'profile' | 'project' | 'quest'

const emit = defineEmits<{
  (e: 'navigate', page: Page): void
}>()

const PROJECTS = Array.from({ length: 6 }, (_, i) => ({
  id: i + 1,
  title: 'Gavity console game_',
  description: "This project isn't anything serious. It's a challenge to myself, to see if I can make a console game experimenting with mechanics. I hope someone will enjoy my work.",
  tags: [['C#', '#5500ff'], ['Web', '#3cb4ff'], ['Pro', '#3cb4ff']] as const,
  reactions: ['127_', '127_', '127_'],
}))
</script>

<template>
  <div class="max-w-[1440px] mx-auto px-10 py-10">
    <SearchBar />
    <div class="flex flex-col gap-5">
      <ProjectCard
        v-for="(p, i) in PROJECTS"
        :key="p.id"
        :p="p"
        @click="emit('navigate', 'project')"
        class="project-item-fade"
        :style="{ animationDelay: `${i * 60}ms` }"
      />
    </div>
  </div>
</template>

<style scoped>
.project-item-fade {
  animation: fadeInUp 0.4s ease-out both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
