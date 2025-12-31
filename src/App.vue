<script setup lang="ts">

  import { onMounted } from 'vue';
  import AOS from 'aos';
  import 'aos/dist/aos.css';
  import Home from './views/Home.vue'
  import Background from './components/Background.vue'
  import Navbar from './components/Navbar.vue'
  import About from './views/About.vue'
  import Project from './components/Project.vue'
  import Contact from './views/Contact.vue'
  import Footer from './components/Footer.vue'

  onMounted(() => {
  AOS.init({
    duration: 1000,
    easing: 'ease-in-out',
    once: true, // Animation only happens once
  });
});
</script>

<template>
  <div class="relative min-h-screen bg-[#1d2029] text-white flex flex-col items-center justify-center overflow-x-hidden">
    <Background />
    
    <Navbar />
    <Home />
    <About /> 
    <Project />
    <Contact />
    <Footer />
  </div>
  
</template>

<style scoped></style>
