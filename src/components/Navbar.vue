<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isOpen = ref(false)

const links = [
  { name: 'About', href: '#about' },
  { name: 'Expertise', href: '#skills' },
  { name: 'Workflow', href: '#ai-stack' },
  { name: 'Experience', href: '#timeline' },
  { name: 'Work', href: '#projects' },
]

// Prevent scrolling when mobile menu is open
const toggleMenu = () => {
  isOpen.value = !isOpen.value
  if (isOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
}

// Close menu when clicking a link
const closeMenu = () => {
  isOpen.value = false
  document.body.style.overflow = ''
}
</script>

<template>
  <nav class="fixed w-full top-0 z-50 bg-white/80 backdrop-blur-md border-b border-zinc-200/80 transition-all duration-300">
    <div class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12 h-16 sm:h-20 flex justify-between items-center">
      
      <!-- Brand Logo -->
      <a href="#" class="text-xl font-bold tracking-tighter text-zinc-900 z-50 relative" @click="closeMenu">
        [Kakvey.DEV]<span class="text-zinc-400">.</span>
      </a>
      
      <!-- Desktop Navigation -->
      <div class="hidden lg:flex space-x-8 text-sm font-medium text-zinc-500">
        <a v-for="link in links" :key="link.name" :href="link.href" class="hover:text-zinc-900 transition-colors">
          {{ link.name }}
        </a>
      </div>
      
      <!-- Desktop CTA Button -->
      <a href="https://t.me/VKak_vey" target="_blank" class="hidden lg:inline-flex items-center justify-center px-5 py-2.5 text-sm font-medium text-white bg-zinc-900 rounded-full hover:bg-zinc-800 transition-colors">
        Let's Talk
      </a>

      <!-- Mobile Hamburger Button -->
      <button @click="toggleMenu" class="lg:hidden p-2 -mr-2 text-zinc-600 hover:text-zinc-900 focus:outline-none z-50 relative">
        <span class="sr-only">Open main menu</span>
        <!-- Hamburger Icon -->
        <svg v-if="!isOpen" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
        <!-- Close (X) Icon -->
        <svg v-else class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
        </svg>
      </button>
    </div>

    <!-- Mobile Menu Overlay -->
    <div 
      class="lg:hidden fixed inset-0 w-full h-screen bg-white/95 backdrop-blur-xl flex flex-col items-center justify-center space-y-8 transition-all duration-300 ease-in-out z-40"
      :class="isOpen ? 'opacity-100 visible translate-y-0' : 'opacity-0 invisible -translate-y-4 pointer-events-none'"
    >
      <a 
        v-for="link in links" 
        :key="link.name" 
        :href="link.href" 
        @click="closeMenu" 
        class="text-2xl font-bold text-zinc-600 hover:text-zinc-900 transition-colors"
      >
        {{ link.name }}
      </a>
      <a 
        href="#contact" 
        @click="closeMenu" 
        class="mt-6 px-8 py-3.5 text-lg font-medium text-white bg-zinc-900 rounded-full hover:bg-zinc-800 transition-colors shadow-lg"
      >
        Let's Talk
      </a>
    </div>
  </nav>
</template>