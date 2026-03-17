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
      { name: 'JavaScript (ES6+)', icon: 'javascript' },
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
      { name: 'System Automation', icon: 'gnubash' },
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
  <section id="skills" class="scroll-mt-32" ref="skillsSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-start">
      
      <!-- Section Header -->
      <div 
        class="lg:col-span-4 opacity-0"
        :class="{ 'animate-slide-up': isVisible }"
        style="animation-delay: 0ms;"
      >
        <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Expertise</h2>
        <h3 class="text-3xl font-bold text-zinc-900">Technical Arsenal.</h3>
      </div>

      <!-- Skills Grid -->
      <div class="lg:col-span-8 grid grid-cols-1 md:grid-cols-2 gap-10">
        <div 
          v-for="(category, index) in skillCategories" 
          :key="category.title"
          class="opacity-0"
          :class="{ 'animate-slide-up': isVisible }"
          :style="{ animationDelay: `${index * 150 + 100}ms` }"
        >
          <h4 class="text-sm font-semibold text-zinc-900 border-b border-zinc-200 pb-2 mb-4">{{ category.title }}</h4>
          
          <ul class="flex flex-wrap gap-2.5">
            <li 
              v-for="(skill, skillIndex) in category.skills" 
              :key="skill.name"
              class="opacity-0 flex items-center gap-2.5 px-3 py-1.5 bg-white border border-zinc-200 rounded-lg text-sm font-medium text-zinc-600 hover:text-zinc-900 hover:border-zinc-300 transition-all cursor-default shadow-sm hover:shadow-md hover:-translate-y-1"
              :class="{ 'animate-slide-up': isVisible }"
              :style="{ animationDelay: `${(index * 150) + (skillIndex * 50) + 300}ms` }"
            >
              <!-- Pulls the SVG icon from simpleicons.org colored to zinc-600 (52525b) -->
              <img :src="`https://cdn.simpleicons.org/${skill.icon}/52525b`" class="w-4 h-4" :alt="skill.name" />
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
    transform: translateY(30px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-slide-up {
  animation: slideUpFade 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>