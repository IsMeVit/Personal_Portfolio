<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue';

interface NavItem {
  name: string;
  href: string;
}

const isMenuOpen = ref<boolean>(false);
const isVisible = ref<boolean>(true);
const scrollY = ref<number>(0);
const lastScrollPosition = ref<number>(0);

const navItems: NavItem[] = [
  { name: 'Home', href: '#home' },
  { name: 'About', href: '#about' },
  { name: 'Projects', href: '#project' },
  { name: 'Contact', href: '#contact' },
];

const navStyle = computed(() => {
  const opacity = Math.min(scrollY.value / 400, 0.6); 
  const blur = Math.min(scrollY.value / 50, 20);      
  return {
    backgroundColor: `rgba(0, 0, 0, ${0.2 + opacity})`,
    backdropFilter: `blur(${10 + blur}px)`,
  };
});

const handleScroll = (): void => {
  const current = window.pageYOffset || document.documentElement.scrollTop;
  if (current < 0) return;
  if (isMenuOpen.value) return;

  const diff = current - lastScrollPosition.value;
  if (Math.abs(diff) < 40) return;

  isVisible.value = diff < 0 || current < 50;
  lastScrollPosition.value = current;
};

onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }));
onUnmounted(() => window.removeEventListener('scroll', handleScroll));

</script>

<template>
  <header 
    class="fixed top-0 left-0 w-full z-50 pt-6 px-4 transition-all duration-700 ease-[cubic-bezier(0.23,1,0.32,1)]"
    :class="isVisible ? 'translate-y-0 opacity-100' : '-translate-y-full opacity-0'"
  >
    <div class="max-w-5xl mx-auto flex flex-col items-center">
      
      <div class="w-full flex justify-end lg:hidden mb-4">
        <button
          @click="isMenuOpen = !isMenuOpen"
          class="p-4 rounded-2xl text-white transition-all active:scale-90 bg-white/10 border border-white/20 backdrop-blur-md"
        >
          <div class="w-6 h-5 flex flex-col justify-between items-center relative">
            <span class="w-full h-0.5 bg-current transition-all duration-300" :class="isMenuOpen ? 'rotate-45 translate-y-2' : ''"></span>
            <span class="w-full h-0.5 bg-current transition-all duration-300" :class="isMenuOpen ? 'opacity-0' : ''"></span>
            <span class="w-full h-0.5 bg-current transition-all duration-300" :class="isMenuOpen ? '-rotate-45 -translate-y-2' : ''"></span>
          </div>
        </button>
      </div>

      <nav 
        :style="navStyle"
        class="flex flex-col lg:flex-row items-center px-2 py-2 lg:px-6 lg:py-2 gap-1 lg:gap-4 rounded-4xl border border-white/10 shadow-[0_8px_32px_0_rgba(0,0,0,0.3)] transition-all duration-500 w-full lg:w-auto"
        :class="isMenuOpen ? 'max-h-100 opacity-100' : 'max-h-0 opacity-0 lg:max-h-full lg:opacity-100 overflow-hidden lg:overflow-visible'"
      >
        <a
          v-for="item in navItems"
          :key="item.name"
          :href="item.href"
          @click="isMenuOpen = false"
          class="relative px-5 py-2.5 text-[17px] font-medium text-white/70 hover:text-white transition-all duration-300 group rounded-full hover:bg-white/5"
        >
          {{ item.name }}
          <span class="absolute inset-x-4 bottom-1 h-px bg-[#9f85ff] scale-x-0 group-hover:scale-x-100 transition-transform duration-500 ease-out"></span>
        </a>

        <div class="hidden lg:block w-px h-4 bg-white/10 mx-2"></div>

        <a 
          href="https://github.com/IsMeVit" 
          target="_blank"
          class="px-5 py-2.5 text-sm font-semibold text-[#9f85ff] hover:bg-[#9f85ff] hover:text-white rounded-full transition-all duration-300 border border-[#9f85ff]/20 hover:border-[#9f85ff]"
        >
          Github
        </a>
      </nav>
    </div>
  </header>
</template>