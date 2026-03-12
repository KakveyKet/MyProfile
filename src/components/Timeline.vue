<script setup>
const timelineEvents = [
  {
    date: '2023 — Present',
    title: 'Freelance Full Stack Developer',
    description: 'Architecting custom web applications, API integrations, and e-commerce solutions for a global client base.'
  },
  {
    date: '2022 — 2023',
    title: 'Automation & Systems Engineer',
    description: 'Designed internal tools, including an Automatic Invoice Splitter and Auto File Downloader, dramatically improving operational efficiency.'
  },
  {
    date: '2021 — 2022',
    title: 'Frontend Web Developer',
    description: 'Developed scalable user interfaces using Vue.js and modern CSS frameworks for tech startups.'
  }
]
</script>

<template>
  <section id="timeline" class="scroll-mt-32">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-start">
      
      <div class="lg:col-span-4">
        <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Experience</h2>
        <h3 class="text-3xl font-bold text-zinc-900">Career Journey.</h3>
      </div>

      <div class="lg:col-span-8">
        <div class="relative border-l border-zinc-200 pl-8 space-y-12 ml-2">
          <div v-for="(event, index) in timelineEvents" :key="index" class="relative group">
            <!-- Sleek indicator dot -->
            <div class="absolute -left-[37px] top-1.5 h-2.5 w-2.5 rounded-full bg-zinc-300 group-hover:bg-zinc-900 transition-colors ring-4 ring-zinc-50"></div>
            
            <span class="text-xs font-semibold text-zinc-400 tracking-widest uppercase mb-1 block">{{ event.date }}</span>
            <h4 class="text-xl font-bold text-zinc-900 mb-2">{{ event.title }}</h4>
            <p class="text-zinc-600 font-light leading-relaxed max-w-2xl">{{ event.description }}</p>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>