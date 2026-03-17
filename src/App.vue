<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Timeline from './components/Timeline.vue'
import Portfolio from './components/Portfolio.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
import AIStack from './components/AIStack.vue'
</script>

<template>
  <!-- 
    Added 'relative' and changed background to be slightly transparent (bg-zinc-50/80) 
    so the animated background can show through. 
  -->
  <div class="relative min-h-screen bg-zinc-50/50 text-zinc-900 font-sans selection:bg-zinc-200 selection:text-zinc-900 overflow-hidden">
    
    <!-- Modern Animated Background -->
    <div class="fixed inset-0 z-[-1] pointer-events-none">
      <div class="absolute top-0 left-1/4 w-96 h-96 bg-blue-200/50 rounded-full mix-blend-multiply filter blur-[100px] opacity-70 animate-blob"></div>
      <div class="absolute top-1/4 right-1/4 w-96 h-96 bg-purple-200/50 rounded-full mix-blend-multiply filter blur-[100px] opacity-70 animate-blob animation-delay-2000"></div>
      <div class="absolute -bottom-32 left-1/3 w-96 h-96 bg-indigo-200/50 rounded-full mix-blend-multiply filter blur-[100px] opacity-70 animate-blob animation-delay-4000"></div>
    </div>

    <Navbar />
    
    <main class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12 py-12 space-y-40 relative z-10">
      <Hero />
      <About />
      <Skills />
      <AIStack />
      <Timeline />
      <Portfolio />
      <Contact />
    </main>

    <Footer />
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
}
body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Custom Animation Keyframes for the blobs */
@keyframes blob {
  0% {
    transform: translate(0px, 0px) scale(1);
  }
  33% {
    transform: translate(30px, -50px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }
  100% {
    transform: translate(0px, 0px) scale(1);
  }
}

.animate-blob {
  animation: blob 15s infinite alternate ease-in-out;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

.animation-delay-4000 {
  animation-delay: 4s;
}
</style>