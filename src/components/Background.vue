<script setup>
import { ref, onMounted, watch } from 'vue';

const props = defineProps({
  starCount: { type: Number, default: 100 },
  accentColor: { type: String, default: '#A855F7' }, // Pass currentTheme.accent here
  mouseX: { type: Number, default: 0 },
  mouseY: { type: Number, default: 0 }
});

const starShapes = ['•', '✦', '✧', '+', '★'];
const stars = ref([]);

const generateStars = () => {
  stars.value = Array.from({ length: props.starCount }, (_, index) => ({
    id: index,
    shape: starShapes[Math.floor(Math.random() * starShapes.length)],
    left: Math.random() * 100,
    top: Math.random() * 100,
    size: 0.5 + Math.random() * 1.5,
    duration: 3 + Math.random() * 4,
    delay: Math.random() * 5,
    // Depth factor: higher means moves more with mouse
    depth: 0.5 + Math.random() * 2 
  }));
};

onMounted(() => {
  generateStars();
});
</script>

<template>
  <div class="absolute inset-0 overflow-hidden pointer-events-none z-0">
    <div
      v-for="star in stars"
      :key="star.id"
      class="absolute transition-transform duration-700 ease-out"
      :style="{ 
        left: `${star.left}%`, 
        top: `${star.top}%`, 
        color: props.accentColor,
        fontSize: `${star.size}rem`,
        opacity: 0.4,
        animation: `twinkle ${star.duration}s infinite ${star.delay}s`,
        // This creates the Parallax effect
        transform: `translate(${(props.mouseX - 500) * 0.01 * star.depth}px, ${(props.mouseY - 500) * 0.01 * star.depth}px)`
      }"
    >
      {{ star.shape }}
    </div>
  </div>
</template>

<style scoped>
@keyframes twinkle {
  0%, 100% { opacity: 0.1; transform: scale(0.8); }
  50% { opacity: 0.8; transform: scale(1.2); }
}

/* Optimization: Make stars look like glowy points */
.absolute {
  text-shadow: 0 0 10px currentColor;
}
</style>