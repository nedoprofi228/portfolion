<script setup lang="ts">
import Tag from '@/components/common/Tag.vue'
import CommentItem from '@/components/comments/CommentItem.vue'
import IconStar from '@/components/icons/IconStar.vue'
import IconUsers from '@/components/icons/IconUsers.vue'
import IconComment from '@/components/icons/IconComment.vue'

const q = { 
  id: 1, 
  title: 'Создайте консольный чат_', 
  desc: 'Вам необходимо создать консольное приложение которое предоставляет доступ к возможности общения с помощью протоколов udp или tcp.', 
  tags: [['C#','#5500ff'],['Web','#3cb4ff'],['Pro','#49307c'],['Hard','#ff9809']] as const, 
  xp: '500  XP', 
  stars: 3, 
  users: '99+', 
  border: '#ff9809', 
  done: false 
}

const COMMENTS = [
  {
    author: 'Aboba123', role: 'pro', roleColor: '#49307c', time: '13:34 16.03.2026',
    text: 'Блин вообще прикольно получилось, мне нравится',
    replies: [
      { author: 'Прогер', role: 'newbie', roleColor: '#00abb1', time: '17:21 16.03.2026', text: 'Мне кажется вообще калл какой-то' },
      { author: 'Aboba123', role: 'pro', roleColor: '#49307c', time: '19:57 16.03.2026', text: 'сам ты калл, не нравится не смотри' },
    ],
  },
  {
    author: 'Qen', role: 'pro', roleColor: '#49307c', time: '13:34 16.03.2026',
    text: 'Блин вообще прикольно получилось, мне нравится. оаоаоаоаоаоаоаоаоаоао просто лучшее что я видел вообще бомба пушка имба',
    replies: [
      { author: 'Прогер', role: 'newbie', roleColor: '#00abb1', time: '17:21 16.03.2026', text: 'реальноооооооооооооооооооооооо броуууууууууууу' },
      { author: 'Aboba123', role: 'pro', roleColor: '#49307c', time: '19:57 16.03.2026', text: 'мне тоже нравится' },
    ],
  },
]
</script>

<template>
  <div class="max-w-[1440px] mx-auto px-10 py-10">
    <!-- Quest card (large) -->
    <div
      class="relative rounded-2xl p-8 mb-10"
      :style="{
        background: '#0d1117',
        border: `1px solid ${q.border}`,
        boxShadow: `0 0 40px ${q.border}22`
      }"
    >
      <div class="absolute inset-[8px] rounded-xl pointer-events-none border border-[#d5d5d5]/15" />

      <div class="flex items-start justify-between mb-4">
        <div class="flex gap-1.5">
          <Tag v-for="tag in q.tags" :key="tag[0]" :label="tag[0]" :color="tag[1]" />
        </div>
        <div class="flex items-center gap-3">
          <div class="flex items-center gap-2 px-3 py-1 rounded" style="background: #3f09ac">
            <span class="text-[#25ed13] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ q.xp }}</span>
          </div>
          <div class="flex items-center gap-1.5 px-3 py-1 rounded" style="background: #49307c">
            <IconStar />
            <span class="text-[#ff9809] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ q.stars }}</span>
          </div>
          <div class="flex items-center gap-1.5 text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
            <IconUsers />
            <span>{{ q.users }}</span>
          </div>
        </div>
      </div>

      <div class="flex items-start gap-2 mb-4">
        <span class="text-2xl mt-1" :style="{ color: q.border, fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">›</span>
        <h1 class="text-4xl font-normal" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace`, color: '#ff9809' }">{{ q.title }}</h1>
      </div>

      <p class="text-[#d5d5d5] text-2xl leading-relaxed mb-5 pl-7" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ q.desc }}</p>

      <div class="flex justify-end">
        <div class="flex items-center gap-2 text-[#d5d5d5] text-2xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
          <IconComment />
          <span>127_</span>
        </div>
      </div>
    </div>

    <!-- Comments -->
    <div class="max-w-3xl">
      <h2 class="text-[#d5d5d5] text-2xl mb-4" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Комментарии</h2>
      <CommentItem v-for="(c, i) in COMMENTS" :key="i" :c="c" />
    </div>
  </div>
</template>
