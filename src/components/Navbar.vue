<script setup>
import { ref, onMounted } from 'vue'

const isOpen = ref(false)
const isDark = ref(false)

const links = [
  { name: 'About', href: '#about' },
  { name: 'Expertise', href: '#skills' },
  { name: 'Workflow', href: '#ai-stack' },
  { name: 'Experience', href: '#timeline' },
  { name: 'Work', href: '#projects' },
]

// --- Dark Mode Logic ---
const toggleDark = () => {
  isDark.value = !isDark.value
  if (isDark.value) {
    document.documentElement.classList.add('dark')
    localStorage.setItem('theme', 'dark')
  } else {
    document.documentElement.classList.remove('dark')
    localStorage.setItem('theme', 'light')
  }
}

onMounted(() => {
  // Check local storage or system preference on load
  if (localStorage.getItem('theme') === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }
})

// --- Mobile Menu Logic ---
const toggleMenu = () => {
  isOpen.value = !isOpen.value
  document.body.style.overflow = isOpen.value ? 'hidden' : ''
}

const closeMenu = () => {
  isOpen.value = false
  document.body.style.overflow = ''
}
</script>

<template>
  <nav
    class="fixed w-full top-0 z-50 bg-white/80 dark:bg-zinc-950/80 backdrop-blur-md border-b border-zinc-200/80 dark:border-zinc-800/80 transition-colors duration-300">
    <div class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12 h-16 sm:h-20 flex justify-between items-center">

      <!-- Brand Logo -->
      <a href="#"
        class="text-xl font-bold tracking-tighter text-zinc-900 dark:text-white z-50 relative transition-colors"
        @click="closeMenu">
        Kakvey<span class="text-zinc-400">.DEV</span>
      </a>

      <!-- Desktop Navigation -->
      <div class="hidden lg:flex space-x-8 text-sm font-medium text-zinc-500 dark:text-zinc-400">
        <a v-for="link in links" :key="link.name" :href="link.href"
          class="hover:text-zinc-900 dark:hover:text-white transition-colors">
          {{ link.name }}
        </a>
      </div>

      <!-- Desktop Right Actions -->
      <div class="hidden lg:flex items-center space-x-4">

        <!-- Dark Mode Toggle -->
        <button @click="toggleDark"
          class="p-2 rounded-full text-zinc-500 hover:bg-zinc-100 dark:text-zinc-400 dark:hover:bg-zinc-800 transition-colors focus:outline-none">
          <!-- Sun Icon (shows in Dark Mode) -->
          <svg v-if="isDark" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z">
            </path>
          </svg>
          <!-- Moon Icon (shows in Light Mode) -->
          <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"></path>
          </svg>
        </button>

        <a href="#contact"
          class="inline-flex items-center justify-center px-5 py-2.5 text-sm font-medium text-white dark:text-zinc-900 bg-zinc-900 dark:bg-white rounded-full hover:bg-zinc-800 dark:hover:bg-zinc-200 transition-colors shadow-sm">
          Let's Talk
        </a>
      </div>

      <!-- Mobile Right Actions -->
      <div class="flex lg:hidden items-center space-x-2 z-50 relative">
        <button @click="toggleDark" class="p-2 text-zinc-500 dark:text-zinc-400 focus:outline-none">
          <svg v-if="isDark" class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z">
            </path>
          </svg>
          <svg v-else class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"></path>
          </svg>
        </button>

        <button @click="toggleMenu"
          class="p-2 -mr-2 text-zinc-600 dark:text-zinc-300 hover:text-zinc-900 dark:hover:text-white focus:outline-none">
          <span class="sr-only">Open main menu</span>
          <svg v-if="!isOpen" class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
          </svg>
          <svg v-else class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Menu Overlay -->
    <div
      class="lg:hidden fixed inset-0 w-full h-screen bg-white/95 dark:bg-zinc-950/95 backdrop-blur-xl flex flex-col items-center justify-center space-y-8 transition-all duration-300 ease-in-out z-40"
      :class="isOpen ? 'opacity-100 visible translate-y-0' : 'opacity-0 invisible -translate-y-4 pointer-events-none'">
      <a v-for="link in links" :key="link.name" :href="link.href" @click="closeMenu"
        class="text-2xl font-bold text-zinc-600 dark:text-zinc-300 hover:text-zinc-900 dark:hover:text-white transition-colors">
        {{ link.name }}
      </a>
      <a href="#contact" @click="closeMenu"
        class="mt-6 px-8 py-3.5 text-lg font-medium text-white dark:text-zinc-900 bg-zinc-900 dark:bg-white rounded-full transition-colors shadow-lg">
        Let's Talk
      </a>
    </div>
  </nav>
</template>