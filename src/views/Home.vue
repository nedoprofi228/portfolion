<script setup lang="ts">
import NewsCard from '@/components/cards/NewsCard.vue'
import BestProjectCard from '@/components/cards/BestProjectCard.vue'

// Import assets
import imgProj1 from '@/assets/console-game-1.png'
import imgProj2 from '@/assets/console-game-2.png'
import imgProj3 from '@/assets/console-game-3.png'
import imgProj4 from '@/assets/console-game-4.png'
import imgProj5 from '@/assets/console-game-5.png'

import imgWeek1 from '@/assets/udp-chat-1.png'
import imgWeek2 from '@/assets/udp-chat-2.png'
import imgWeek3 from '@/assets/udp-chat-3.png'

type Page = 'home' | 'projects' | 'quests' | 'profile' | 'project' | 'quest'

const emit = defineEmits<{
  (e: 'navigate', page: Page): void
}>()

const NEWS = [
  { id: 1, title: 'Обновление эвентов_', text: 'Полностью переделана система ивентов. Теперь каждый пользователь может поучаствовать в нем. Также переделана система вознаграждения пользователей за победу в эвентах.', comments: '137_', border: '#00e8d4' },
  { id: 2, title: 'SpaceInvertion event_', text: 'В этом эвенте вам предстоит окунуться в мир космоса и придумать, а также реализовать приложения в стиле и с геймплеем космоса и солнечных систем.', comments: '1291_', border: '#ea00ff', tags: [['C#', '#5500ff'], ['Unity', '#009dff'], ['Hard', '#ff9809']] as const },
  { id: 3, title: 'Исправлен баг с клонированием проектов_', text: 'Теперь вы можете смело клонировать чужие проекты других пользователей, смотрите чужие проекты с удовольствием!', comments: '137_', border: '#00e8d4' },
  { id: 4, title: 'Обновление эвентов_', text: 'Полностью переделана система ивентов. Теперь каждый пользователь может поучаствовать в нем. Также переделана система вознаграждения пользователей за победу в эвентах.', comments: '137_', border: '#00e8d4' },
] as const

const bestOfAllTimeImgs = [imgProj1, imgProj2, imgProj3, imgProj4, imgProj5]
const bestOfWeekImgs = [imgWeek1, imgWeek2, imgWeek3]
</script>

<template>
  <div>
    <!-- Hero -->
    <section class="flex flex-col items-center justify-center py-20 text-center">
      <h1
        class="text-[#d5d5d5] text-5xl font-normal mb-4 hero-title"
        :style="{ fontFamily: `'Intel One Mono', 'JetBrains Mono', monospace` }"
      >
        PortFolion
      </h1>
      <p
        class="text-[#d5d5d5] text-xl max-w-2xl"
        :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
      >
        Хвастайся, смейся или создавай свои пет проекты которыми не жалко поделиться ^_^
      </p>
      <div class="mt-8 text-[#d5d5d5]/60">
        <div class="animate-bounce">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round">
            <path d="M12 5v14M5 12l7 7 7-7" />
          </svg>
        </div>
      </div>
    </section>

    <!-- Content -->
    <div class="max-w-[1440px] mx-auto px-10 pb-20">
      <div class="flex gap-10">
        <!-- News feed -->
        <div class="flex-1 flex flex-col gap-5">
          <NewsCard
            v-for="item in NEWS"
            :key="item.id"
            :item="item"
          />
        </div>

        <!-- Sidebar -->
        <div class="w-[380px] flex-shrink-0 flex flex-col gap-8">
          <div>
            <h3 class="text-[#d5d5d5] text-2xl mb-4 flex items-center gap-2" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
              <svg width="28" height="28" viewBox="0 0 40 40" fill="none" stroke="#d5d5d5" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <path d="M20 4l4 12h12l-10 7.5 4 12L20 28l-10 7.5 4-12L4 16h12z" />
              </svg>
              Лучший за все время:
            </h3>
            <BestProjectCard
              title="Консольная игра_"
              author="Qpro_"
              :imgs="bestOfAllTimeImgs"
              :reactions="['127_', '127_', '127_']"
              @click="emit('navigate', 'project')"
            />
          </div>
          <div>
            <h3 class="text-[#d5d5d5] text-2xl mb-4 flex items-center gap-2" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
              <svg width="28" height="28" viewBox="0 0 40 40" fill="none" stroke="#d5d5d5" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="20" cy="20" r="14" />
                <path d="M20 10v10l6 4" />
              </svg>
              Лучший за неделю:
            </h3>
            <BestProjectCard
              title="UDP chat_"
              author="LittleCode_"
              :imgs="bestOfWeekImgs"
              :reactions="['127_', '127_', '127_']"
              @click="emit('navigate', 'project')"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.hero-title {
  animation: fadeInDown 0.5s ease-out 0.1s both;
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
