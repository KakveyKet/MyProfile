<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Timeline from './components/Timeline.vue'
import Portfolio from './components/Portfolio.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="min-h-screen bg-zinc-50 text-zinc-900 font-sans selection:bg-zinc-200 selection:text-zinc-900">
    <Navbar />
    
    <main class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12 py-12 space-y-40">
      <Hero />
      <About />
      <Skills />
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
</style>