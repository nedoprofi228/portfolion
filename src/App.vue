<script setup lang="ts">
import { ref, computed } from 'vue'
import Header from '@/components/layout/Header.vue'
import Footer from '@/components/layout/Footer.vue'

// Import views
import Home from '@/views/Home.vue'
import Projects from '@/views/Projects.vue'
import Quests from '@/views/Quests.vue'
import Profile from '@/views/Profile.vue'
import ProjectDetail from '@/views/ProjectDetail.vue'
import QuestDetail from '@/views/QuestDetail.vue'

type Page = 'home' | 'projects' | 'quests' | 'profile' | 'project' | 'quest'

const page = ref<Page>('home')

const navigate = (p: Page) => {
  page.value = p
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const activeView = computed(() => {
  switch (page.value) {
    case 'home': return Home
    case 'projects': return Projects
    case 'quests': return Quests
    case 'profile': return Profile
    case 'project': return ProjectDetail
    case 'quest': return QuestDetail
    default: return Home
  }
})
</script>

<template>
  <div class="min-h-screen bg-[#010409] flex flex-col justify-between">
    <Header :page="page" @navigate="navigate" />
    <main class="pt-16 flex-grow">
      <Transition name="fade-slide" mode="out-in">
        <component :is="activeView" :key="page" @navigate="navigate" />
      </Transition>
    </main>
    <Footer />
  </div>
</template>

<style>
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(18px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-12px);
}
</style>
