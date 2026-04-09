<script setup>
import { ref, onMounted } from 'vue'

const skillsSection = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.1 })
  if (skillsSection.value) observer.observe(skillsSection.value)
})

const skillCategories = [
  { title: 'Frontend Development', skills: [{ name: 'Vue.js', icon: 'vuedotjs' }, { name: 'React', icon: 'react' }, { name: 'JavaScript', icon: 'javascript' }, { name: 'Tailwind CSS', icon: 'tailwindcss' }, { name: 'HTML5/CSS3', icon: 'html5' }] },
  { title: 'Backend & Databases', skills: [{ name: 'Node.js', icon: 'nodedotjs' }, { name: 'Laravel', icon: 'laravel' }, { name: 'Python', icon: 'python' }, { name: 'Django', icon: 'django' }, { name: 'REST APIs', icon: 'postman' }, { name: 'MySQL', icon: 'mysql' }, { name: 'MongoDB', icon: 'mongodb' }] },
  { title: 'Tools & Architecture', skills: [{ name: 'Git & GitHub', icon: 'github' }, { name: 'Figma', icon: 'figma' }, { name: 'System Auto', icon: 'gnubash' }, { name: 'Agile/Scrum', icon: 'jira' }] },
  { title: 'WordPress & CMS', skills: [{ name: 'WordPress', icon: 'wordpress' }, { name: 'Elementor', icon: 'elementor' }, { name: 'WooCommerce', icon: 'woocommerce' }, { name: 'SureForm', icon: 'typeform' }, { name: 'Custom Plugins', icon: 'php' }] }
]
</script>

<template>
  <section id="skills" class="scroll-mt-24 sm:scroll-mt-32 transition-colors duration-500" ref="skillsSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start">
      
      <div class="lg:col-span-4 lg:sticky lg:top-32 relative">
        <div class="opacity-0" :class="{ 'animate-slide-up': isVisible }" style="animation-delay: 0ms;">
          <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Expertise</h2>
          <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 dark:text-white tracking-tight transition-colors">Technical Arsenal.</h3>
          <p class="mt-6 text-zinc-500 dark:text-zinc-400 font-light leading-relaxed max-w-sm transition-colors">
            The programming languages, frameworks, and tools I leverage to build robust, scalable, and automated digital products.
          </p>
          <div class="hidden lg:block w-12 h-1 bg-zinc-200 dark:bg-zinc-800 mt-8 rounded-full transition-colors"></div>
        </div>
      </div>

      <div class="lg:col-span-8 grid grid-cols-1 md:grid-cols-2 gap-6 sm:gap-8">
        <div v-for="(category, index) in skillCategories" :key="category.title" class="p-6 sm:p-8 rounded-3xl bg-white dark:bg-zinc-900/50 border border-zinc-200/60 dark:border-zinc-800 shadow-sm hover:shadow-xl hover:shadow-zinc-200/50 dark:hover:shadow-zinc-900/50 transition-all duration-500 opacity-0 group" :class="{ 'animate-slide-up': isVisible }" :style="{ animationDelay: `${index * 150 + 150}ms` }">
          <div class="flex items-center mb-6">
            <h4 class="text-lg font-bold text-zinc-900 dark:text-zinc-100 transition-colors">{{ category.title }}</h4>
            <div class="flex-1 h-px bg-zinc-100 dark:bg-zinc-800 ml-4 transition-colors"></div>
          </div>
          
          <ul class="flex flex-wrap gap-2.5 sm:gap-3">
            <li v-for="(skill, skillIndex) in category.skills" :key="skill.name" class="opacity-0 flex items-center gap-2.5 px-3.5 py-2 bg-zinc-50/80 dark:bg-zinc-800/50 border border-zinc-200/80 dark:border-zinc-700/80 rounded-xl text-sm font-semibold text-zinc-600 dark:text-zinc-300 hover:text-blue-600 dark:hover:text-white hover:bg-white dark:hover:bg-zinc-700 hover:border-blue-200 dark:hover:border-blue-500/50 hover:shadow-sm transition-all duration-300 cursor-default hover:-translate-y-0.5" :class="{ 'animate-slide-up': isVisible }" :style="{ animationDelay: `${(index * 150) + (skillIndex * 50) + 300}ms` }">
              <!-- dark:invert makes the icon white in dark mode! -->
              <img :src="`https://cdn.simpleicons.org/${skill.icon}/52525b`" class="w-4 h-4 opacity-70 group-hover:opacity-100 dark:invert dark:opacity-80 transition-all" :alt="skill.name" />
              {{ skill.name }}
            </li>
          </ul>
        </div>
      </div>

    </div>
  </section>
</template>

<style scoped>
@keyframes slideUpFade {
  from { opacity: 0; transform: translateY(30px) scale(0.98); }
  to { opacity: 1; transform: translateY(0) scale(1); }
}
.animate-slide-up { animation: slideUpFade 0.7s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
</style>