<script setup>
const links = [
  { name: 'About', href: '#about' },
  { name: 'Expertise', href: '#skills' },
  { name: 'Experience', href: '#timeline' },
  { name: 'Work', href: '#projects' },
]
</script>

<template>
  <nav class="fixed w-full top-0 z-50 bg-white/80 backdrop-blur-md border-b border-zinc-200/80 transition-all duration-300">
    <div class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12 h-20 flex justify-between items-center">
      <a href="#" class="text-xl font-bold tracking-tighter text-zinc-900">
        Kakvey Ket<span class="text-zinc-400">.</span>
      </a>
      
      <div class="hidden md:flex space-x-8 text-sm font-medium text-zinc-500">
        <a v-for="link in links" :key="link.name" :href="link.href" class="hover:text-zinc-900 transition-colors">
          {{ link.name }}
        </a>
      </div>
      
      <a href="#contact" class="hidden md:inline-flex items-center justify-center px-5 py-2.5 text-sm font-medium text-white bg-zinc-900 rounded-full hover:bg-zinc-800 transition-colors">
        Let's Talk
      </a>
    </div>
  </nav>
</template>