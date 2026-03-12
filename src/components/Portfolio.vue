<script setup>
const projects = [
  {
    title: 'ERP Automation Suite',
    type: 'Internal Tooling',
    description: 'A robust Python & Django tool designed to automatically parse, split, and process enterprise invoices, eliminating manual data entry.',
    tags: ['Python', 'Django', 'Automation'],
    link: '#'
  },
  {
    title: 'E-Commerce Platform',
    type: 'Web Application',
    description: 'A high-performance storefront built with Vue 3 and Tailwind CSS, featuring a custom shopping cart and real-time inventory management.',
    tags: ['Vue.js', 'Tailwind', 'Node.js'],
    link: '#'
  },
  {
    title: 'Khmer 404',
    type: 'Digital Content',
    description: 'Educational platform providing resources, tutorials, and insights into modern web development and software architecture.',
    tags: ['Content', 'Web Dev'],
    link: '#'
  }
]
</script>

<template>
  <section id="projects" class="scroll-mt-32">
    <div class="mb-16">
      <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Selected Work</h2>
      <h3 class="text-3xl font-bold text-zinc-900">Featured Projects.</h3>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <a v-for="(project, index) in projects" :key="index" :href="project.link" class="group flex flex-col h-full">
        <!-- Minimalist Image Area -->
        <div class="h-56 bg-zinc-100 rounded-2xl overflow-hidden mb-6 relative border border-zinc-200/60">
          <div class="absolute inset-0 bg-zinc-900/0 group-hover:bg-zinc-900/5 transition-colors duration-300"></div>
          <!-- Placeholder pattern or image goes here -->
          <div class="w-full h-full flex items-center justify-center text-zinc-300">
             <svg class="w-10 h-10 group-hover:scale-110 transition-transform duration-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path></svg>
          </div>
        </div>
        
        <!-- Typography & Content -->
        <div class="flex-1 flex flex-col">
          <p class="text-xs font-bold text-zinc-400 uppercase tracking-wider mb-2">{{ project.type }}</p>
          <h4 class="text-xl font-bold text-zinc-900 mb-3 group-hover:text-zinc-600 transition-colors">{{ project.title }}</h4>
          <p class="text-zinc-500 font-light mb-6 flex-1">{{ project.description }}</p>
          
          <div class="flex flex-wrap gap-2 mt-auto">
            <span v-for="tag in project.tags" :key="tag" class="text-xs font-medium text-zinc-500 bg-zinc-100 px-2.5 py-1 rounded-md">
              {{ tag }}
            </span>
          </div>
        </div>
      </a>
    </div>
  </section>
</template>