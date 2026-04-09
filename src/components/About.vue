<script setup>
import { ref, onMounted } from 'vue'

const aboutSection = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.1 })

  if (aboutSection.value) observer.observe(aboutSection.value)
})

const educationData = [
  {
    title: 'Information Technology',
    institution: 'National University of Battambang',
    detail: 'Graduated 2025',
    iconColor: 'text-blue-600 dark:text-blue-400',
    iconBg: 'bg-blue-50 dark:bg-blue-500/10',
    iconPath: 'M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4'
  },
  {
    title: 'Chinese Language',
    institution: 'Kong Zi Institute',
    detail: 'HSK 3 Certification',
    iconColor: 'text-emerald-600 dark:text-emerald-400',
    iconBg: 'bg-emerald-50 dark:bg-emerald-500/10',
    iconPath: 'M21 12a9 9 0 01-9 9m9-9a9 9 0 00-9-9m9 9H3m9 9a9 9 0 01-9-9m9 9c1.657 0 3-4.03 3-9s-1.343-9-3-9m0 18c-1.657 0-3-4.03-3-9s1.343-9 3-9m-9 9a9 9 0 019-9'
  },
  {
    title: 'English Language',
    institution: 'Professional Working Proficiency',
    detail: 'Intermediate Level',
    iconColor: 'text-violet-600 dark:text-violet-400',
    iconBg: 'bg-violet-50 dark:bg-violet-500/10',
    iconPath: 'M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z'
  }
]
</script>

<template>
  <section id="about" class="scroll-mt-24 sm:scroll-mt-32 transition-colors duration-500" ref="aboutSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start">

      <div class="lg:col-span-4 lg:sticky lg:top-32 relative">
        <div class="opacity-0" :class="{ 'animate-slide-up': isVisible }" style="animation-delay: 0ms;">
          <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">About</h2>
          <h3
            class="text-3xl sm:text-4xl font-extrabold text-zinc-900 dark:text-white tracking-tight transition-colors">
            Engineering with purpose.</h3>
          <div class="hidden lg:block w-12 h-1 bg-zinc-200 dark:bg-zinc-800 mt-8 rounded-full transition-colors"></div>
        </div>
      </div>

      <div class="lg:col-span-8">
        <div
          class="space-y-6 text-base sm:text-lg text-zinc-600 dark:text-zinc-400 font-light leading-relaxed mb-12 opacity-0 transition-colors"
          :class="{ 'animate-slide-up': isVisible }" style="animation-delay: 150ms;">
          <p>I am a dedicated full-stack developer with a passion for building complete, end-to-end web solutions. From
            crafting responsive user interfaces to designing robust database architectures, I focus on delivering
            seamless digital experiences.</p>
          <p>Recently, my focus has shifted toward building automated internal tools and ERP integrations that save
            teams hundreds of hours of manual work. I believe that great software should solve real business problems
            efficiently and elegantly.</p>
        </div>

        <div class="space-y-4">
          <div v-for="(item, index) in educationData" :key="index"
            class="group flex flex-col sm:flex-row items-start sm:items-center p-5 sm:p-6 rounded-2xl bg-zinc-50/50 dark:bg-zinc-900/50 border border-zinc-200/60 dark:border-zinc-800 hover:bg-white dark:hover:bg-zinc-800/80 hover:shadow-lg hover:shadow-zinc-200/50 dark:hover:shadow-none hover:border-zinc-300 dark:hover:border-zinc-700 transition-all duration-300 opacity-0"
            :class="{ 'animate-slide-up': isVisible }" :style="{ animationDelay: `${(index * 150) + 300}ms` }">
            <div
              :class="[`p-3.5 rounded-xl shadow-sm border border-white/50 dark:border-white/5 mb-4 sm:mb-0 sm:mr-6 flex-shrink-0 transition-all duration-300 group-hover:scale-110 group-hover:-rotate-3`, item.iconBg, item.iconColor]">
              <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="item.iconPath"></path>
              </svg>
            </div>

            <div class="flex-1">
              <h4 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-1">Academic Background</h4>
              <p
                class="text-lg font-bold text-zinc-900 dark:text-zinc-100 mb-0.5 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors">
                {{ item.title }}</p>
              <div
                class="flex flex-col sm:flex-row sm:items-center text-sm font-medium text-zinc-500 dark:text-zinc-500 gap-1 sm:gap-2">
                <span>{{ item.institution }}</span>
                <span class="hidden sm:inline text-zinc-300 dark:text-zinc-700">&bull;</span>
                <span class="text-zinc-400">{{ item.detail }}</span>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<style scoped>
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