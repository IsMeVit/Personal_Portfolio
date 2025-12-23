<script setup>
const skillCategories = [
  {title: "Frontend",icon: "✨",skills: ["Html", "CSS", "Vue", "React", "Next.js", "Tailwind"],},
  { title: "Backend", icon: "☄️", skills: ["Node", "Express", "PostgreSQL"] },
  { title: "Programming", icon: "🛰️", skills: ["C++", "Python", "JavaScript", 'TypeScript'] },
  { title: "Remote", icon: "☁️", skills: ["GitHub", "Git", "Vercel"] },
];
</script>

<template>
  <div
    data-aos="fade-left" data-aos-delay="200"
    class ="min-h-screen flex items-center justify-center p-4 md:p-10 relative z-10"
  >
    <div
      class="max-w-5xl w-full flex flex-col md:grid md:grid-cols-12 gap-6 my-10"
    >
      <section class="md:col-span-4 space-y-6">
        <div
          class="bg-white/10 backdrop-blur-xl border border-white/20 rounded-[2.5rem] p-8 flex flex-col items-center text-center shadow-2xl"
        >
          <div class="relative mb-6">
            <div
              class="absolute inset-0 bg-purple-500 blur-3xl opacity-20 rounded-full"
            ></div>
            <img
              src="/Img/pf.jpg"
              alt="Dara Davit"
              class="relative w-32 h-32 rounded-3xl object-cover border-2 border-white/20 shadow-2xl"
            />
          </div>
          <h1 class="text-2xl font-black text-white tracking-tight">
            Dara Davit
          </h1>
          <p
            class="text-purple-400 text-xs font-mono mb-6 uppercase tracking-[0.2em]"
          >
            Frontend Developer
          </p>

          <a
            href="https://github.com/IsMeVit"
            target="_blank"
            class="w-full py-3 px-4 bg-white/5 hover:bg-white text-white hover:text-black border border-white/10 rounded-2xl text-sm font-bold transition-all active:scale-95 flex items-center justify-center gap-2"
          >
            <span>GitHub</span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path
                d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
              ></path>
            </svg>
          </a>
        </div>

        <div
          class="bg-white/5 backdrop-blur-xl border border-white/10 rounded-[2.5rem] p-8 shadow-xl group hover:border-blue-500/30 transition-all"
        >
          <div class="flex items-center justify-between mb-8">
            <div class="flex items-center gap-4">
              <div
                class="p-3 bg-blue-500/20 rounded-2xl text-2xl group-hover:rotate-12 transition-transform"
              >
                🎓
              </div>
              <div>
                <h3 class="text-white font-bold text-lg tracking-tight">
                  Academic Journey
                </h3>
                <p
                  class="text-blue-400 text-xs font-mono uppercase tracking-widest leading-none mt-1"
                >
                  Computer Science Major
                </p>
              </div>
            </div>
            <div
              class="hidden sm:block px-4 py-1.5 bg-blue-500/10 border border-blue-500/20 rounded-full text-blue-300 text-[10px] font-bold uppercase tracking-tighter"
            >
              In Progress
            </div>
          </div>

          <div
            class="relative ml-4 pl-8 border-l-2 border-white/10 space-y-10 pb-2"
          >
            <div class="relative">
              <div
                class="absolute -left-10.25 top-1 w-5 h-5 rounded-full bg-blue-500/20 border-4 border-black flex items-center justify-center"
              >
                <div
                  class="w-2 h-2 rounded-full bg-blue-400 shadow-[0_0_12px_rgba(96,165,250,1)]"
                ></div>
              </div>
              <div
                class="flex flex-col sm:flex-row sm:justify-between sm:items-center gap-1"
              >
                <p
                  class="text-white font-black text-sm uppercase tracking-wide"
                >
                  PPIU University
                </p>
                <span
                  class="text-[10px] font-mono text-blue-300 bg-blue-400/10 px-2 py-0.5 rounded"
                  >2024 — Present</span
                >
              </div>
              <p class="text-gray-400 text-xs mt-1">
                Transferred to continue advanced Software Engineering studies.
              </p>
            </div>

            <div class="relative">
              <div
                class="absolute -left-10.25 top-1 w-5 h-5 rounded-full bg-white/5 border-4 border-black flex items-center justify-center"
              >
                <div class="w-2 h-2 rounded-full bg-gray-600"></div>
              </div>
              <div
                class="flex flex-col sm:flex-row sm:justify-between sm:items-center gap-1"
              >
                <p
                  class="text-gray-300 font-bold text-sm uppercase tracking-wide"
                >
                  Brachnasastra Technology University
                </p>
                <span class="text-[10px] font-mono text-gray-500"
                  >2023 — 2024</span
                >
              </div>
              <p class="text-gray-500 text-xs mt-1 italic">
                Foundation of Computer Science & Algorithms.
              </p>
            </div>
          </div>

          <div class="mt-8 pt-6 border-t border-white/5">
            <div class="flex justify-between items-center mb-3">
              <span
                class="text-[10px] font-black text-gray-500 uppercase tracking-widest"
                >Total Credits Progress</span
              >
              <span class="text-blue-400 font-mono text-xs">Year 3</span>
            </div>
            <div class="h-2 w-full bg-white/5 rounded-full p-0.5">
              <div
                class="h-full w-[75%] bg-linear-to-r from-blue-600 to-indigo-400 rounded-full shadow-[0_0_15px_rgba(37,99,235,0.4)]"
              ></div>
            </div>
          </div>
        </div>
      </section>

      <section class="md:col-span-8 space-y-6">
        <div
          class="bg-white/5 backdrop-blur-lg border border-white/10 rounded-[2.5rem] p-8 shadow-xl"
        >
          <h2
            class="text-indigo-300 font-mono text-[10px] uppercase tracking-[0.4em] mb-4"
          >
            Biography
          </h2>
          <p class="text-gray-200 text-xl leading-relaxed font-medium">
            I’m a 19-year-old
            <span
              class="text-white font-black underline decoration-purple-500 underline-offset-4"
              >Computer Science student</span
            >
            at PPIU. I build modern web experiences with a focus on clean code
            and interactive design.
          </p>
        </div>

        <div>
          <h2
            class="text-center mb-6 text-2xl font-black tracking-tighter text-white flex items-center justify-center gap-4"
          >
            <span
              class="h-px w-12 bg-linear-to-r from-transparent to-white/20"
            ></span>
            Expertise
            <span
              class="h-px w-12 bg-linear-to-l from-transparent to-white/20"
            ></span>
          </h2>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div
              v-for="cat in skillCategories"
              :key="cat.title"
              class="bg-white/5 backdrop-blur-md border border-white/10 rounded-4xl p-6 hover:bg-white/[0.07] hover:border-purple-500/30 transition-all group"
            >
              <div class="flex items-center justify-between mb-4">
                <h3 class="text-white font-bold flex items-center gap-3">
                  <span
                    class="p-2 bg-white/5 rounded-lg text-lg group-hover:scale-110 transition-transform"
                    >{{ cat.icon }}</span
                  >
                  <span class="text-sm tracking-wide">{{ cat.title }}</span>
                </h3>
              </div>

              <div class="flex flex-wrap gap-2">
                <span
                  v-for="skill in cat.skills"
                  :key="skill"
                  class="text-[10px] font-mono py-1.5 px-3 bg-black/20 text-gray-400 rounded-xl group-hover:text-white group-hover:bg-purple-500/20 border border-white/5 transition-all"
                >
                  {{ skill }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
@media (min-width: 768px) {
  section {
    animation: float 6s ease-in-out infinite;
  }
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

section:nth-child(2) {
  animation-delay: 1s;
}

@keyframes gradient-text {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.animate-gradient-text {
  animation: gradient-text 4s ease infinite;
}
</style>
