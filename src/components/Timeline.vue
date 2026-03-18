<script setup>
import { ref, onMounted } from 'vue'

// 1. Setup Intersection Observer for scroll animations
const timelineSection = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      observer.disconnect() // Stop observing once it has animated in
    }
  }, {
    threshold: 0.1 // Triggers when 10% of the section is visible
  })

  if (timelineSection.value) {
    observer.observe(timelineSection.value)
  }
})

// 2. Timeline Experience Data
const timelineEvents = [
  {
    date: '2025 - Present',
    title: 'Working at Trax Appareal Cambodia at Phnom Penh as Programmer (Local Young Talent)',
    description: 'Based on the project requirement, I convert the manual work to use the technology to save time and make the system or RPA auto work. I also study about the bussiness process and flow about the factory to make the system (Export Management System, Inventory Management System, and etc) that can help the company to save time and make the work more efficient.'
  },
  {
    date: '2024 - 2025',
    title: 'Working as Front end Developer at Battambang (Master IT Co., Ltd.)',
    description: 'Based on the project requirement, I developed the front end of the web app using Vue.js, React.js, and Tailwind CSS. I also collaborated with the backend team to integrate APIs and ensure seamless functionality. And also using WordPress to build the website for company and client too.'
  },
  {
    date: '2022 — 2023',
    title: 'Intern as IT Support & Web Developer',
    description: 'Developed internal scanning attendance & controlling the computer lab and report about the inventory of the computer lab. Training the staff and students to use the system. And also developed the website for the University to use the E-Learning platform and E-library.'
  },
  {
    date: '2022',
    title: 'Web App Developer Intern',
    description: 'Integrated Glide App with Webhook to build a web app for managing inventory and sales data, streamlining operations for a local business.'
  },
  {
    date: '2021',
    title: 'Teaching and Lead the classmate',
    description: 'Teaching about web dev programming such as HTML, CSS, JavaScript, Tailwind CSS, and React.js to the classmate and also lead the classmate to do the project together.'
  }
]
</script>

<template>
  <section id="timeline" class="scroll-mt-24 sm:scroll-mt-32" ref="timelineSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start">

      <!-- Left Column: Section Header (Sticky on Desktop) -->
      <div class="lg:col-span-4 lg:sticky lg:top-32 relative">
        <div 
          class="opacity-0"
          :class="{ 'animate-slide-up': isVisible }"
          style="animation-delay: 0ms;"
        >
          <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Experience</h2>
          <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 tracking-tight">Career Journey.</h3>
          
          <p class="mt-6 text-zinc-500 font-light leading-relaxed max-w-sm">
            A chronological timeline of my professional experience, internships, and leadership roles in software engineering and development.
          </p>
          
          <!-- Decorative subtle line -->
          <div class="hidden lg:block w-12 h-1 bg-zinc-200 mt-8 rounded-full"></div>
        </div>
      </div>

      <!-- Right Column: Timeline Content -->
      <div class="lg:col-span-8">
        <!-- Timeline Line Container -->
        <div class="relative border-l-2 border-zinc-100 sm:ml-4 ml-2">
          
          <!-- Timeline Items -->
          <div 
            v-for="(event, index) in timelineEvents" 
            :key="index" 
            class="relative pl-6 sm:pl-10 pb-12 last:pb-0 group opacity-0"
            :class="{ 'animate-slide-up': isVisible }"
            :style="{ animationDelay: `${index * 150 + 150}ms` }"
          >
            
            <!-- Sleek Interactive Indicator Dot -->
            <div class="absolute -left-[9px] top-2 h-4 w-4 rounded-full bg-white border-4 border-zinc-200 group-hover:border-blue-600 group-hover:bg-blue-600 transition-all duration-300 shadow-sm z-10"></div>

            <!-- Content Card -->
            <div class="bg-zinc-50/50 p-6 sm:p-8 rounded-3xl border border-zinc-200/60 hover:bg-white hover:shadow-xl hover:shadow-zinc-200/50 hover:border-zinc-300 transition-all duration-500 hover:-translate-y-1 relative overflow-hidden">
              
              <!-- Subtle decorative corner accent -->
              <div class="absolute -top-12 -right-12 w-24 h-24 bg-blue-50 rounded-full blur-2xl opacity-0 group-hover:opacity-100 transition-opacity duration-500 pointer-events-none"></div>

              <!-- Date Badge -->
              <span class="inline-block px-3 py-1 mb-4 text-[10px] sm:text-xs font-bold text-zinc-500 uppercase tracking-widest bg-white border border-zinc-200 rounded-full shadow-sm group-hover:text-blue-600 group-hover:border-blue-100 transition-colors">
                {{ event.date }}
              </span>
              
              <!-- Title & Description -->
              <h4 class="text-lg sm:text-xl font-bold text-zinc-900 mb-3 group-hover:text-zinc-800 transition-colors leading-snug">
                {{ event.title }}
              </h4>
              <p class="text-sm sm:text-base text-zinc-500 font-light leading-relaxed">
                {{ event.description }}
              </p>
              
            </div>
            
          </div>
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
/* Custom Keyframe animation for the slide-up fade effect */
@keyframes slideUpFade {
  from {
    opacity: 0;
    transform: translateY(30px) scale(0.98);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-slide-up {
  animation: slideUpFade 0.7s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>