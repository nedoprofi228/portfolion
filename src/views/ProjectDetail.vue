<script setup lang="ts">
import { ref } from 'vue'
import Tag from '@/components/common/Tag.vue'
import CommentItem from '@/components/comments/CommentItem.vue'
import IconHeart from '@/components/icons/IconHeart.vue'
import IconFork from '@/components/icons/IconFork.vue'
import IconShare from '@/components/icons/IconShare.vue'
import IconComment from '@/components/icons/IconComment.vue'
import IconChevron from '@/components/icons/IconChevron.vue'
import IconFile from '@/components/icons/IconFile.vue'
import IconFolder from '@/components/icons/IconFolder.vue'
import IconCopy from '@/components/icons/IconCopy.vue'

// Import assets
import imgMain from '@/assets/project-main.png'
import imgThumb1 from '@/assets/project-thumb1.png'
import imgThumb2 from '@/assets/project-thumb2.png'
import imgThumb3 from '@/assets/project-thumb3.png'

const SLIDES = [imgMain, imgThumb1, imgThumb2, imgThumb3]

const FILES = [
  { name: 'GameObjectInterfaces.cs', type: 'file', link: 'https://github.com/nedoprofi228/CSharp-Console-Game/blob/main/ConsoleApp1/GameObjectInterfaces.cs' },
  { name: 'ConsoleApp1.csproj', type: 'file', link: 'https://github.com/nedoprofi228/CSharp-Console-Game/blob/main/ConsoleApp1/ConsoleApp1.csproj' },
  { name: 'Character.cs', type: 'file', link: 'https://github.com/nedoprofi228/CSharp-Console-Game/blob/main/ConsoleApp1/Character.cs' },
  { name: 'bin/Debug/net8.0', type: 'folder', link: 'https://github.com/nedoprofi228/CSharp-Console-Game/tree/main/ConsoleApp1/bin/Debug/net8.0' },
  { name: 'obj', type: 'folder', link: 'https://github.com/nedoprofi228/CSharp-Console-Game/tree/main/ConsoleApp1/obj' },
  { name: '.vs', type: 'folder', link: 'https://github.com/nedoprofi228/CSharp-Console-Game/tree/main/ConsoleApp1/.vs' },
  { name: 'entities', type: 'folder' },
  { name: 'services', type: 'folder' },
]

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

const slide = ref(0)
const copied = ref(false)
const gitUrl = 'git clone https://github.com/nedoprofi228/CSharp-Console-Game'

const copy = () => {
  navigator.clipboard.writeText(gitUrl)
  copied.value = true
  setTimeout(() => {
    copied.value = false
  }, 2000)
}

const prevSlide = () => {
  slide.value = (slide.value - 1 + SLIDES.length) % SLIDES.length
}

const nextSlide = () => {
  slide.value = (slide.value + 1) % SLIDES.length
}
</script>

<template>
  <div class="max-w-[1440px] mx-auto px-10 py-10">
    <!-- Title -->
    <div class="mb-6">
      <div class="flex items-center gap-2 mb-3">
        <span class="text-[#d5d5d5]/60 text-3xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">›</span>
        <h1 class="text-[#d5d5d5] text-4xl font-normal" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">Gavity console game_</h1>
      </div>
      <p class="text-[#d5d5d5] text-2xl leading-relaxed" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
        This project isn't anything serious. It's a challenge to myself, to see if I can make a console game experimenting with mechanics. I hope someone will enjoy my work.
      </p>
    </div>

    <!-- Main card -->
    <div class="bg-[#0d1117] rounded-2xl p-8 mb-8">
      <!-- Tech tags -->
      <div class="flex items-center justify-between mb-6">
        <div class="flex gap-2">
          <Tag v-for="[l, c] in [['С#', '#5500ff'], ['Console', '#3cb4ff'], ['dotnet', '#ff09b5']]" :key="l" :label="l" :color="c" />
        </div>
        <div class="flex gap-2">
          <Tag v-for="[l, c] in [['Interesting', '#0284e2'], ['Easy', '#069220']]" :key="l" :label="l" :color="c" />
        </div>
      </div>

      <!-- Image slider -->
      <div class="relative rounded-2xl overflow-hidden mb-4 bg-[#020812]" style="height: 480px">
        <Transition name="slide-fade" mode="out-in">
          <img
            :key="slide"
            :src="SLIDES[slide]"
            class="w-full h-full object-cover"
            alt="slide"
          />
        </Transition>
        
        <!-- Prev button -->
        <button
          @click="prevSlide"
          class="absolute left-4 top-1/2 -translate-y-1/2 w-14 h-14 rounded-full flex items-center justify-center cursor-pointer hover:bg-white/35 active:scale-95 transition-all duration-150"
          style="background: rgba(217, 217, 217, 0.2)"
        >
          <div style="transform: rotate(180deg)"><IconChevron dir="right" /></div>
        </button>
        
        <!-- Next button -->
        <button
          @click="nextSlide"
          class="absolute right-4 top-1/2 -translate-y-1/2 w-14 h-14 rounded-full flex items-center justify-center cursor-pointer hover:bg-white/35 active:scale-95 transition-all duration-150"
          style="background: rgba(217, 217, 217, 0.2)"
        >
          <IconChevron dir="right" />
        </button>
      </div>

      <!-- Thumbnails -->
      <div class="flex gap-3 mb-8">
        <button
          v-for="(img, i) in SLIDES"
          :key="i"
          @click="slide = i"
          class="rounded-xl overflow-hidden border-2 transition-colors cursor-pointer hover:scale-105 transition-all duration-150"
          :style="{
            borderColor: slide === i ? '#633dff' : 'transparent',
            width: '120px',
            height: '80px'
          }"
        >
          <img :src="img" class="w-full h-full object-cover" alt="thumbnail" />
        </button>
      </div>

      <!-- File tree -->
      <div class="bg-[#020812] rounded-2xl overflow-hidden mb-6">
        <div
          v-for="(f, i) in FILES"
          :key="i"
          class="flex items-center gap-3 px-5 py-3.5 border-b border-[#6e6363]/50 last:border-0 hover:bg-white/5 transition-colors duration-100"
        >
          <IconFile v-if="f.type === 'file'" />
          <IconFolder v-else />
          <a
            v-if="f.link"
            :href="f.link"
            target="_blank"
            rel="noreferrer"
            class="text-[#d5d5d5] text-sm underline hover:text-white transition-colors"
            :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
          >
            {{ f.name }}
          </a>
          <span
            v-else
            class="text-[#d5d5d5] text-sm"
            :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }"
          >
            {{ f.name }}
          </span>
        </div>
        
        <!-- Git clone -->
        <div class="flex items-center gap-3 px-5 py-3 bg-[#0d1117]">
          <div class="w-px h-4 bg-white/30" />
          <span class="text-[#d5d5d5] text-sm flex-1" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">{{ gitUrl }}</span>
          <button @click="copy" class="p-1 cursor-pointer hover:scale-110 active:scale-95 transition-transform duration-100">
            <span v-if="copied" class="text-[#25ed13] text-xs" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">скопировано!</span>
            <IconCopy v-else />
          </button>
        </div>
      </div>

      <!-- Reactions -->
      <div class="flex items-center justify-end gap-8">
        <div class="flex items-center gap-5">
          <button class="flex items-center gap-1.5 text-[#d5d5d5] hover:text-white cursor-pointer hover:scale-110 active:scale-95 transition-all duration-150">
            <IconHeart red />
            <span class="text-2xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">127_</span>
          </button>
          <button class="flex items-center gap-1.5 text-[#d5d5d5] hover:text-white cursor-pointer hover:scale-110 active:scale-95 transition-all duration-150">
            <IconFork />
            <span class="text-2xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">127_</span>
          </button>
          <button class="flex items-center gap-1.5 text-[#d5d5d5] hover:text-white cursor-pointer hover:scale-110 active:scale-95 transition-all duration-150">
            <IconShare />
            <span class="text-2xl" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">127_</span>
          </button>
        </div>
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

<style scoped>
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.3s ease;
}
.slide-fade-enter-from {
  opacity: 0;
  transform: translateX(40px);
}
.slide-fade-leave-to {
  opacity: 0;
  transform: translateX(-40px);
}
</style>
