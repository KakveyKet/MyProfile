<script setup>
import { ref, onMounted } from 'vue'

// 1. Setup Intersection Observer for scroll animations
const skillsSection = ref(null)
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

  if (skillsSection.value) {
    observer.observe(skillsSection.value)
  }
})

// 2. Updated data structure to include simpleicon slugs
const skillCategories = [
  {
    title: 'Frontend Development',
    skills: [
      { name: 'Vue.js', icon: 'vuedotjs' },
      { name: 'React', icon: 'react' },
      { name: 'JavaScript', icon: 'javascript' },
      { name: 'Tailwind CSS', icon: 'tailwindcss' },
      { name: 'HTML5/CSS3', icon: 'html5' }
    ]
  },
  {
    title: 'Backend & Databases',
    skills: [
      { name: 'Node.js', icon: 'nodedotjs' },
      { name: 'Laravel', icon: 'laravel' },
      { name: 'Python', icon: 'python' },
      { name: 'Django', icon: 'django' },
      { name: 'REST APIs', icon: 'postman' },
      { name: 'MySQL', icon: 'mysql' },
      { name: 'MongoDB', icon: 'mongodb' }
    ]
  },
  {
    title: 'Tools & Architecture',
    skills: [
      { name: 'Git & GitHub', icon: 'github' },
      { name: 'Figma', icon: 'figma' },
      { name: 'System Auto', icon: 'gnubash' },
      { name: 'Agile/Scrum', icon: 'jira' }
    ]
  },
  {
    title: 'WordPress & CMS',
    skills: [
      { name: 'WordPress', icon: 'wordpress' },
      { name: 'Elementor', icon: 'elementor' },
      { name: 'WooCommerce', icon: 'woocommerce' },
      { name: 'SureForm', icon: 'typeform' },
      { name: 'Custom Plugins', icon: 'php' }
    ]
  }
]
</script>

<template>
  <section id="skills" class="scroll-mt-24 sm:scroll-mt-32" ref="skillsSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start">
      
      <!-- Left Column: Section Header (Sticky on Desktop) -->
      <div class="lg:col-span-4 lg:sticky lg:top-32 relative">
        <div 
          class="opacity-0"
          :class="{ 'animate-slide-up': isVisible }"
          style="animation-delay: 0ms;"
        >
          <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Expertise</h2>
          <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 tracking-tight">Technical Arsenal.</h3>
          
          <p class="mt-6 text-zinc-500 font-light leading-relaxed max-w-sm">
            The programming languages, frameworks, and tools I leverage to build robust, scalable, and automated digital products.
          </p>
          
          <!-- Decorative subtle line -->
          <div class="hidden lg:block w-12 h-1 bg-zinc-200 mt-8 rounded-full"></div>
        </div>
      </div>

      <!-- Right Column: Skills Grid -->
      <div class="lg:col-span-8 grid grid-cols-1 md:grid-cols-2 gap-6 sm:gap-8">
        
        <div 
          v-for="(category, index) in skillCategories" 
          :key="category.title"
          class="p-6 sm:p-8 rounded-3xl bg-white border border-zinc-200/60 shadow-sm hover:shadow-xl hover:shadow-zinc-200/50 transition-all duration-500 opacity-0 group"
          :class="{ 'animate-slide-up': isVisible }"
          :style="{ animationDelay: `${index * 150 + 150}ms` }"
        >
          <div class="flex items-center mb-6">
            <h4 class="text-lg font-bold text-zinc-900">{{ category.title }}</h4>
            <div class="flex-1 h-px bg-zinc-100 ml-4"></div>
          </div>
          
          <ul class="flex flex-wrap gap-2.5 sm:gap-3">
            <li 
              v-for="(skill, skillIndex) in category.skills" 
              :key="skill.name"
              class="opacity-0 flex items-center gap-2.5 px-3.5 py-2 bg-zinc-50/80 border border-zinc-200/80 rounded-xl text-sm font-semibold text-zinc-600 hover:text-blue-600 hover:bg-white hover:border-blue-200 hover:shadow-sm transition-all duration-300 cursor-default hover:-translate-y-0.5"
              :class="{ 'animate-slide-up': isVisible }"
              :style="{ animationDelay: `${(index * 150) + (skillIndex * 50) + 300}ms` }"
            >
              <!-- Pulls the SVG icon from simpleicons.org colored to zinc-600 (52525b) -->
              <img :src="`https://cdn.simpleicons.org/${skill.icon}/52525b`" class="w-4 h-4 opacity-70 group-hover:opacity-100 transition-opacity" :alt="skill.name" />
              {{ skill.name }}
            </li>
          </ul>
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