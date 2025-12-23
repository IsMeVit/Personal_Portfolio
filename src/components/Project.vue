<script lang="ts" setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

const currentIndex = ref(0)
const isMobile = ref(false)

// 1. Screen Resize Logic
const updateScreen = () => {
  isMobile.value = window.innerWidth < 768
}

onMounted(() => {
  updateScreen()
  window.addEventListener('resize', updateScreen)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateScreen)
})

// 2. Data
const projects = [
  {
    title: "Vue-calculator",
    description: "A functional calculator built to demonstrate state management and component architecture.",
    tech: ['Vue.js', 'Vuex', 'Tailwind CSS'],
    link: "https://calculator-vue-omega.vercel.app/"
  },
  {
    title: "UX/UI Design project",
    description: "Comprehensive school project focusing on user research, wireframing, and interactive prototyping.",
    tech: ['Figma'],
    link: "https://www.figma.com/proto/..."
  },
  {
    title: "Todo list",
    description: "A task management application featuring persistence and TypeScript for type safety.",
    tech: ['Vue.js', 'TypeScript', 'Tailwind CSS'],
    link: "https://todo-list-eta-five-32.vercel.app/"
  },
  {
    title: "Something New...",
    description: "An upcoming project exploring backend integration with Firebase and real-time data.",
    tech: ['Vue.js', 'Vuex', 'Tailwind CSS', 'Firebase'],
    link: "#"
  }
]

// 3. Sliding Logic
const itemsPerView = computed(() => (isMobile.value ? 1 : 2))
const maxIndex = computed(() => projects.length - itemsPerView.value)

const slideWidth = computed(() => (isMobile.value ? 100 : 50))
const translateX = computed(() => `translateX(-${currentIndex.value * slideWidth.value}%)`)

const nextSlide = () => {
  if (currentIndex.value < maxIndex.value) {
    currentIndex.value++
  } else {
    currentIndex.value = 0 // Loop back to start
  }
}

const prevSlide = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--
  } else {
    currentIndex.value = maxIndex.value // Loop to end
  }
}

const goToSlide = (index: number) => {
  // Ensure we don't go past the limit on desktop
  currentIndex.value = Math.min(index, maxIndex.value)
}
</script>

<template>
  <div 
    data-aos="fade-up" 
    class="mt-10 min-h-screen w-full overflow-hidden font-[Space-Mono] text-white relative z-10 px-4 py-10"
  >
    <h1 id="project" class="text-center text-4xl md:text-5xl font-black mb-12 drop-shadow-[0_0_10px_rgba(168,85,247,0.4)]">
      PROJECTS
    </h1>

    <div class="relative max-w-6xl mx-auto flex items-center group">
      <button 
        @click="prevSlide" 
        class="absolute -left-2 md:-left-6 z-30 p-3 md:p-4 rounded-full bg-white/5 backdrop-blur-md border border-white/10 text-yellow-300 hover:bg-white/20 transition-all active:scale-90"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>
      </button>

      <div class="overflow-hidden w-full px-2">
        <div 
          class="flex transition-transform duration-700 ease-[cubic-bezier(0.25,1,0.5,1)]" 
          :style="{ transform: translateX }"
        >
          <div 
            v-for="(project, index) in projects" 
            :key="index" 
            class="min-w-full md:min-w-[50%] flex justify-center px-4"
          >
            <div class="relative bg-white/10 backdrop-blur-lg border border-white/20 rounded-4xl p-6 md:p-8 w-full max-w-[320px] md:max-w-sm shadow-2xl active:scale-95 transition-transform">
              <div class="flex justify-between items-start mb-4">
                <span class="text-[10px] bg-green-500/20 text-green-400 px-3 py-1 rounded-full border border-green-500/30 font-bold uppercase tracking-wider">
                  Active
                </span>
              </div>

              <h3 class="text-xl md:text-2xl font-bold mb-3 tracking-tight text-white">{{ project.title }}</h3>
              
              <p class="text-gray-400 text-sm leading-relaxed mb-6 h-16 line-clamp-3">
                {{ project.description }}
              </p>
              
              <div class="flex flex-wrap gap-2 mb-8">
                <span v-for="(tech, i) in project.tech" :key="i" 
                      class="bg-white/5 border border-white/10 text-[10px] px-2 py-1 rounded-md text-gray-300">
                  {{ tech }}
                </span>
              </div>
              
              <a 
                :href="project.link" 
                target="_blank" 
                class="relative w-full flex justify-center items-center gap-2 py-3 bg-white text-black rounded-xl font-bold text-sm transition-all duration-300 group/btn hover:bg-black hover:text-white border-2 border-transparent hover:border-purple-500 hover:shadow-[0_0_20px_rgba(168,85,247,0.4)]"
              >
                View Project 
                <svg 
                  xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" 
                  stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"
                  class="group-hover/btn:translate-x-1 group-hover/btn:-translate-y-1 transition-transform"
                >
                  <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/>
                </svg>
              </a>
            </div>
          </div>
        </div>
      </div>

      <button 
        @click="nextSlide" 
        class="absolute -right-2 md:-right-6 z-30 p-3 md:p-4 rounded-full bg-white/5 backdrop-blur-md border border-white/10 text-yellow-300 hover:bg-white/20 transition-all active:scale-90"
      >
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
      </button>
    </div>

    <div class="mt-12 flex items-center justify-center gap-3">
      <span
        v-for="(dot, i) in projects"
        :key="i"
        class="h-2 rounded-full cursor-pointer transition-all duration-500 relative"
        :class="[
          currentIndex === i 
            ? 'w-10 bg-cyan-400 shadow-glow-cyan active-glow' 
            : 'w-2 bg-white/20 hover:bg-white/40'
        ]"
        @click="goToSlide(i)"
      >
        <span v-if="currentIndex === i" class="absolute inset-0 rounded-full bg-white blur-[1px] opacity-40"></span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.shadow-glow-cyan {
  box-shadow: 0 0 15px rgba(34, 211, 238, 0.8), 0 0 30px rgba(34, 211, 238, 0.4);
}

.active-glow {
  animation: pulse-glow-cyan 2.5s infinite ease-in-out;
}

@keyframes pulse-glow-cyan {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.8; transform: scale(0.98); }
}

/* Smooth scrolling for the container if you decide to use touch */
.flex {
  will-change: transform;
  backface-visibility: hidden;
}
</style>