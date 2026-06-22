<script setup lang="ts">
import { ref, onMounted } from 'vue'
import SkillBar from '@/components/profile/SkillBar.vue'
import ProjectCard from '@/components/cards/ProjectCard.vue'
import QuestCard from '@/components/cards/QuestCard.vue'
import IconHeart from '@/components/icons/IconHeart.vue'
import IconFork from '@/components/icons/IconFork.vue'
import IconShare from '@/components/icons/IconShare.vue'

// Import assets
import imgAvatar from '@/assets/user-avatar.png'

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

const QUESTS = [
  { id: 1, title: 'Создайте консольный чат_', desc: 'Вам необходимо создать консольное приложение которое предоставляет доступ к возможности общения с помощью протоколов udp или tcp.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#ff9809', done: false },
  { id: 2, title: 'Создайте 10 проектов_', desc: 'Вам необходимо создать 10 любых проектов, которые соответствуют минимальным требованиями: 10к строк, 10 файлов, структура.', tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, xp: '500  XP', stars: 3, users: '99+', border: '#3cb4ff', done: false },
]

const SKILLS = [
  { lang: 'С#', color: '#5500ff', level: 'Junior', level_n: 1 },
  { lang: 'Web', color: '#3cb4ff', level: 'Middle', level_n: 2 },
  { lang: 'dotnet', color: '#ff09b5', level: 'Middle', level_n: 2 },
  { lang: 'PostgreSql', color: '#ff2c41', level: 'Senior', level_n: 3 },
]

const levelProgressAnimated = ref(false)

onMounted(() => {
  setTimeout(() => {
    levelProgressAnimated.value = true
  }, 100)
})
</script>

<template>
  <div class="max-w-[1440px] mx-auto px-10 py-10">
    <div class="flex gap-8">
      <!-- Left column -->
      <div class="w-[520px] flex-shrink-0 flex flex-col gap-6">
        <!-- User card -->
        <div class="bg-[#0d1117] border border-[#d5d5d5]/30 rounded-2xl p-6">
          <div class="flex flex-col items-center mb-5">
            <div class="w-52 h-52 rounded-full overflow-hidden mb-4 border-2 border-[#d5d5d5]/20 hover:scale-104 transition-transform duration-200">
              <img :src="imgAvatar" class="w-full h-full object-cover" alt="avatar" />
            </div>
            <h2 class="text-2xl text-white font-normal" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Super Progammer312_</h2>
            <span class="text-xl mt-1" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, color: '#5500ff' }">Бог проги</span>
          </div>

          <!-- Level -->
          <div class="flex items-center gap-3 mb-5">
            <svg width="36" height="36" viewBox="0 0 39 39" fill="none" stroke="#FF9809" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="19.5" cy="19.5" r="16" />
              <path d="M19.5 10v10l6 4" />
            </svg>
            <div class="flex-1">
              <div class="flex items-center justify-between mb-1">
                <span class="text-[#ff9809] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">lvl</span>
                <span class="text-[#ff9809] text-2xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">87</span>
              </div>
              <div class="relative h-2 rounded-full bg-[#d9d9d9] overflow-hidden">
                <div
                  class="absolute inset-y-0 left-0 rounded-full bg-[#ff9809] transition-all duration-800 ease-out"
                  :style="{ width: levelProgressAnimated ? '58%' : '0%' }"
                />
              </div>
            </div>
          </div>

          <!-- Tech tags -->
          <h3 class="text-2xl text-white mb-3" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Навыки</h3>
          <div class="flex flex-wrap gap-2 mb-5">
            <span
              v-for="[l, c] in [['С#', '#5500ff'], ['Web', '#3cb4ff'], ['Pro', '#49307c'], ['Hard', '#ff9809'], ['dotnet', '#ff09b5'], ['asp.net core', '#00558b'], ['PosgreSql', '#ff2c41']]"
              :key="l"
              class="px-2 py-0.5 rounded text-sm cursor-default hover:scale-105 transition-transform duration-100"
              :style="{
                fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`,
                color: c,
                border: `1px solid ${c}55`,
                background: `${c}11`
              }"
            >
              {{ l }}
            </span>
          </div>

          <!-- Reactions -->
          <div class="flex items-center gap-6">
            <div class="flex items-center gap-1.5 text-white text-xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
              <IconHeart />
              <span>127</span>
            </div>
            <div class="flex items-center gap-1.5 text-white text-xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
              <IconFork />
              <span>127</span>
            </div>
            <div class="flex items-center gap-1.5 text-white text-xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
              <IconShare />
              <span>127</span>
            </div>
          </div>
        </div>

        <!-- Skill bars -->
        <div class="bg-[#0d1117] border border-[#d5d5d5]/30 rounded-2xl p-6">
          <h3 class="text-2xl text-white mb-5" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Показатель</h3>
          <div class="flex flex-col gap-5">
            <SkillBar
              v-for="s in SKILLS"
              :key="s.lang"
              v-bind="s"
            />
          </div>
        </div>
      </div>

      <!-- Right column -->
      <div class="flex-1 flex flex-col gap-8">
        <div>
          <h2 class="text-2xl text-[#d5d5d5] mb-4" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Проекты</h2>
          <div class="flex flex-col gap-4">
            <ProjectCard
              v-for="p in PROJECTS.slice(0, 3)"
              :key="p.id"
              :p="p"
              @click="emit('navigate', 'project')"
            />
            <button
              @click="emit('navigate', 'projects')"
              class="text-[#6ba8e2] text-xl text-left cursor-pointer hover:translate-x-1 hover:underline transition-all duration-150"
              :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
            >
              больше...
            </button>
          </div>
        </div>

        <div>
          <h2 class="text-2xl text-[#d5d5d5] mb-4" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Выполнение квестов</h2>
          <div class="flex flex-col gap-4">
            <QuestCard
              v-for="q in QUESTS"
              :key="q.id"
              :q="q"
              @click="emit('navigate', 'quest')"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
