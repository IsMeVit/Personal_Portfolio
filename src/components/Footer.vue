<script setup>
import { ref, onMounted } from 'vue'

const currentTime = ref('00:00:00')

const updateTime = () => {
  const now = new Date()
  currentTime.value = now.toLocaleTimeString('en-US', { 
    hour12: false, 
    hour: '2-digit', 
    minute: '2-digit',
    second: '2-digit' 
  })
}

onMounted(() => {
  updateTime()
  setInterval(updateTime, 1000)
})
</script>


<template>
  <footer
  data-aos="fade-enter-active" data-aos-delay="100"
  class="relative w-full pt-20 pb-10 overflow-hidden bg-black/20 border-t border-white/5">
    
    <div 
      class="absolute top-0 left-1/2 -translate-x-1/2 w-1/2 h-px bg-linear-to-r from-transparent via-purple-500/50 to-transparent"
    ></div>

    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
        
        <div class="space-y-4">
          <div class="flex items-center gap-2">
            <div class="h-2 w-2 rounded-full bg-purple-500 shadow-[0_0_8px_#A855F7]"></div>
            <span class="text-white font-black tracking-widest text-sm italic">DARA DAVIT</span>
          </div>
          <p class="text-gray-500 text-[11px] font-mono leading-relaxed uppercase tracking-wider">
            Framework: Vue 3.5+<br/>Github
            Engine: Vite / Tailwind<br/>
            Deployed: Vercel<br/>
            Build: Stable Version
          </p>
        </div>

        <div class="flex flex-col md:items-center">
          <div class="bg-white/3 border border-white/10 rounded-2xl px-6 py-4 backdrop-blur-xl">
            <div class="flex flex-col gap-1">
              <span class="text-[9px] font-mono text-gray-500 uppercase tracking-widest">Local System Time</span>
              <span class="text-white font-mono text-lg tracking-widest">{{ currentTime }}</span>
            </div>
          </div>
        </div>

        <div class="flex flex-col md:items-end gap-4">
          <div class="text-right">
            <span class="text-[10px] font-mono text-purple-400 uppercase tracking-[0.3em]">Build Version</span>
            <p class="text-white text-xl font-black italic tracking-tighter">v2.1.3</p>
          </div>
          <p class="text-gray-600 text-[9px] font-mono tracking-widest uppercase">
            © 2024-2025 All Rights Reserved
          </p>
        </div>

      </div>

      <div class="mt-16 flex justify-center opacity-20 pointer-events-none">
        <span class="text-[8vw] font-black text-transparent border-text italic select-none">
          CREATED_BY_DAVIT
        </span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.border-text {
  -webkit-text-stroke: 1px rgba(255,255,255,0.2);
}
</style>