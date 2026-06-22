<template>
  <footer class="bg-[#0d1117] border-t border-[#d5d5d5]/30 py-4">
    <div class="max-w-[1440px] mx-auto px-10 flex items-center justify-between">
      <div class="flex items-center gap-2 text-[#d5d5d5] text-sm" :style="{ fontFamily: `'Intel One Mono', 'JetBrains Mono', monospace` }">
        <span>© 2026</span>
        <span class="mx-1">·</span>
        <span>PortFolion_</span>
      </div>
      <div class="flex items-center gap-8 text-[#d5d5d5] text-sm" :style="{ fontFamily: `'JetBrains Mono', 'Iosevka Charon Mono', monospace` }">
        <a
          v-for="l in ['Правила', 'Контакты', 'Условия пользования']"
          :key="l"
          href="#"
          class="transition-colors duration-150 hover:text-white"
        >
          {{ l }}
        </a>
      </div>
    </div>
  </footer>
</template>
