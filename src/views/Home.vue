<script setup>
import { ref, onMounted } from 'vue'

const words = ['DAVIT', 'DAVISHH']
const currentWord = ref('')
const greeting = ref('HELLO')
let wordIndex = 0

onMounted(() => {
  typeWord()
})

function typeWord() {
  const word = words[wordIndex]
  let charIndex = 0
  const type = () => {
    if (charIndex <= word.length) {
      currentWord.value = word.slice(0, charIndex++)
      setTimeout(type, 150)
    } else {
      setTimeout(eraseWord, 2500)
    }
  }
  type()
}

function eraseWord() {
  const erase = () => {
    if (currentWord.value.length > 0) {
      currentWord.value = currentWord.value.slice(0, -1)
      setTimeout(erase, 80)
    } else {
      wordIndex = (wordIndex + 1) % words.length
      setTimeout(typeWord, 500)
    }
  }
  erase()
}
</script>


<template>
  <div data-aos="fade-down" data-aos-delay="200"  id="home" class="mb-10 relative h-screen w-full flex items-center justify-center overflow-hidden font-sans">
    
    <div class="absolute inset-0 flex items-center justify-center select-none pointer-events-none">
      <span class="text-[40vw] font-black text-white/2 leading-none border-text">
        {{ currentWord.charAt(0) }}
      </span>
    </div>

    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-125 h-125 bg-purple-600/10 blur-[120px] rounded-full"></div>

    <div class="relative z-10 flex flex-col items-center">
      
      <div class="flex items-center gap-2 mb-6 opacity-0 animate-fade-in">
        <span class="h-px w-8 bg-purple-500"></span>
        <span class="text-purple-400 font-mono text-xs uppercase tracking-[0.4em]">{{ greeting }}</span>
      </div>

      <div class="text-center space-y-2">
        <h2 class="text-gray-500 text-xl md:text-2xl font-medium tracking-tight">It's me</h2>
        
        <h1 class="text-7xl md:text-9xl font-black text-white tracking-tighter transition-all duration-500">
          <span class="relative inline-block">
            {{ currentWord }}
            <span class="absolute bottom-2 left-0 w-full h-2 bg-purple-500/30 -z-10 skew-x-[-15deg]"></span>
          </span>
        </h1>
      </div>

      <div class="mt-12 flex flex-wrap justify-center gap-3 opacity-0 animate-fade-in-up">
        <span class="px-5 py-2 bg-white/5 backdrop-blur-md border border-white/10 rounded-full text-xs font-bold text-gray-300 uppercase tracking-widest hover:border-purple-500/50 transition-colors">
          Developer
        </span>
        <span class="px-5 py-2 bg-white/5 backdrop-blur-md border border-white/10 rounded-full text-xs font-bold text-gray-300 uppercase tracking-widest hover:border-purple-500/50 transition-colors">
          Designer
        </span>
      </div>
    </div>

    <div class="absolute left-10 bottom-10 hidden md:block">
      <div class="flex flex-col gap-4 text-gray-600 text-[10px] font-mono vertical-text tracking-widest">
        <span>EST. 2025</span>
        <div class="h-20 w-px bg-white/10 mx-auto"></div>
        <span>PHNOM PENH</span>
      </div>
    </div>

  </div>
</template>

<style scoped>
.border-text {
  -webkit-text-stroke: 1px rgba(255,255,255,0.05);
  color: transparent;
}

.vertical-text {
  writing-mode: vertical-rl;
  text-orientation: mixed;
}

.animate-fade-in {
  animation: fadeIn 1s ease forwards 0.5s;
}

.animate-fade-in-up {
  animation: fadeInUp 1s ease forwards 1s;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>