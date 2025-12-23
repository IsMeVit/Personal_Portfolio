<script lang="ts" setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

const currentIndex = ref(0)
const ifisMobile = ref(window.innerWidth < 768)

const updateScreen = () => {
  ifisMobile.value = window.innerWidth < 768
}

onMounted(() => {
  window.addEventListener('resize', updateScreen)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateScreen)
})

const slideWidth = computed(() => (ifisMobile.value ? 100 : 50)) // 100% if mobile, 50% if md+
const translateX = computed(() => `translateX(-${currentIndex.value * slideWidth.value}%)`)


const projects = [
  {
    title: "Vue-calculator",
    description: "It's just a basic project.",
    tech: ['Vue.js', 'Vuex', 'Tailwind CSS'],
    link: "https://calculator-vue-omega.vercel.app/"
  },
  {
    title: "UX/UI Design project",
    description: "It's my school project in my UX/UI course.",
    tech: ['Figma'],
    link: "https://www.figma.com/proto/3pIOX8h737NMpMAoxJaylf/Figma-midterm-project-team-...?node-id=57-11&p=f&t=Yue3fzEQAxq2P04V-0&scaling=scale-down&content-scaling=fixed&page-id=0%3A1&starting-point-node-id=272%3A477&show-proto-sidebar=1"
  },
  {
    title: "Todo list",
    description: "Todo list is a simple project to manage your tasks effectively.",
    tech: ['Vue.js', 'TypeScript', 'Tailwind CSS'],
    link: "https://todo-list-eta-five-32.vercel.app/"
  },
  {
    title: "Something New...",
    description: "",
    tech: ['Vue.js', 'Vuex', 'Tailwind CSS', 'Firebase'],
    link: "#"
  }
]
const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + projects.length) % projects.length
}

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % projects.length
}
</script>

<template>
  <div 
  data-aos="fade-enter-active" data-aos-delay="200"
  class="mt-10 min-h-screen w-full overflow-hidden font-[Space-Mono] text-white relative z-10 px-4">
    <h1 id="project" class="text-center text-4xl md:text-5xl font-black mb-8 drop-shadow-[0_0_10px_rgba(168,85,247,0.4)]">
      Projects
    </h1>
  
    <div class="relative max-w-6xl mx-auto flex items-center justify-center">
      <button @click="prevSlide" class="hidden md:flex absolute left-0 z-20 p-4 rounded-full bg-white/5 backdrop-blur-md border border-white/10 text-yellow-300">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>
      </button>

      <div class="overflow-hidden w-full">
        <div 
          class="flex transition-transform duration-500 ease-[cubic-bezier(0.25,1,0.5,1)] touch-pan-y" 
          :style="{ transform: translateX }"
        >
          <div v-for="(project, index) in projects" :key="index" 
               class="min-w-full md:min-w-[50%] flex justify-center px-2 md:px-4">
            
            <div class="relative bg-white/10 backdrop-blur-lg border border-white/20 rounded-4xl p-6 md:p-8 w-full max-w-[320px] md:max-w-sm shadow-2xl active:scale-95 transition-transform">
              
              <div class="flex justify-between items-start mb-4">
                <span class="text-[10px] bg-green-500/20 text-green-400 px-2 py-1 rounded-full border border-green-500/30 font-bold uppercase tracking-wider">Active</span>
              </div>

              <h3 class="text-xl md:text-2xl font-bold mb-2 tracking-tight">{{ project.title }}</h3>
              
              <p class="text-gray-300 text-sm leading-relaxed mb-6 line-clamp-3">
                {{ project.description }}
              </p>
              
              <div class="flex flex-wrap gap-1.5 mb-8">
                <span v-for="(tech, i) in project.tech" :key="i" 
                      class="bg-white/5 border border-white/10 text-[9px] px-2 py-1 rounded-md text-white">
                  {{ tech }}
                </span>
              </div>
              
              <a 
                :href="project.link" 
                target="_blank" 
                class="relative w-full flex justify-center items-center gap-2 py-3 bg-white text-black rounded-xl font-bold text-sm transition-all duration-300 group hover:bg-gray hover:text-purple-400 border-2 border-transparent hover:border-purple-500 hover:shadow-[0_0_20px_rgba(168,85,247,0.6)]"
                >
                <span class="relative z-10 flex items-center gap-2">
                View Project 
                <svg 
                    xmlns="http://www.w3.org/2000/svg" 
                    width="16" 
                    height="16" 
                    viewBox="0 0 24 24" 
                    fill="none" 
                    stroke="currentColor" 
                    stroke-width="3" 
                    stroke-linecap="round" 
                    stroke-linejoin="round"
                    class="group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform duration-300"
                >
                    <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/>
                    <polyline points="15 3 21 3 21 9"/>
                    <line x1="10" y1="14" x2="21" y2="3"/>
                </svg>
                </span>
                </a>
            </div>

          </div>
        </div>
      </div>

      <button @click="nextSlide" class="hidden md:flex absolute right-0 z-20 p-4 rounded-full bg-white/5 backdrop-blur-md border border-white/10 text-yellow-300">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
      </button>
    </div>

    <div class="mt-10 flex flex-col items-center gap-6">
    <p class="text-[10px] text-gray-500 uppercase tracking-[0.3em] md:hidden animate-pulse">
      Swipe to explore
    </p>
    </div>

    <div class="flex justify-center items-center space-x-4">
      <span
        v-for="(dot, i) in projects"
        :key="i"
        class="h-2 rounded-full cursor-pointer transition-all duration-500 relative"
        :class="[
          currentIndex === i 
            ? 'w-10 bg-cyan-400 shadow-glow-cyan active-glow' 
            : 'w-2 bg-white/20 hover:bg-white/40'
        ]"
        @click="currentIndex = i"
      >
        <span 
          v-if="currentIndex === i" 
          class="absolute inset-0 rounded-full bg-white blur-[1px] opacity-60"
        ></span>
      </span>
  </div>

    
    
  </div>
</template>

<style scoped>
.shadow-glow-cyan {
  box-shadow: 
    0 0 15px rgba(34, 211, 238, 0.8), 
    0 0 30px rgba(34, 211, 238, 0.4),
    0 0 45px rgba(34, 211, 238, 0.2);
}

/* Pulsing Animation */
.active-glow {
  animation: pulse-glow-cyan 2.5s infinite ease-in-out;
}

@keyframes pulse-glow-cyan {
  0%, 100% {
    filter: brightness(100%) saturate(100%);
    box-shadow: 
      0 0 15px rgba(34, 211, 238, 0.8), 
      0 0 30px rgba(34, 211, 238, 0.4);
  }
  50% {
    filter: brightness(150%) saturate(200%);
    box-shadow: 
      0 0 25px rgba(34, 211, 238, 1), 
      0 0 50px rgba(34, 211, 238, 0.6),
      0 0 80px rgba(34, 211, 238, 0.3);
  }
}
</style>