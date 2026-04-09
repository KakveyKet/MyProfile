<script setup>
import { ref, onMounted } from 'vue'

const aiSection = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.1 })
  if (aiSection.value) observer.observe(aiSection.value)
})

const aiTools = [
  { name: 'ChatGPT', icon: 'dependabot', description: 'Advanced reasoning, problem-solving, and code architecture assistance.' },
  { name: 'Gemini', icon: 'googlegemini', description: 'Multimodal analysis and deep integration with Google ecosystems.' },
  { name: 'Grok', icon: 'x', description: 'Real-time data synthesis and rapid problem solving.' },
  { name: 'Copilot', icon: 'githubcopilot', description: 'In-IDE contextual code generation and intelligent auto-completion.' },
  { name: 'Webhooks', icon: 'jsonwebtokens', description: 'Automated cross-platform triggers connecting AI to external services.' }
]
</script>

<template>
  <section id="ai-stack" class="scroll-mt-24 sm:scroll-mt-32 transition-colors duration-500" ref="aiSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start">
      
      <div class="lg:col-span-4 lg:sticky lg:top-32 relative">
        <div class="opacity-0" :class="{ 'animate-slide-up': isVisible }" style="animation-delay: 0ms;">
          <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Workflow</h2>
          <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 dark:text-white tracking-tight transition-colors">AI Stack.</h3>
          <p class="mt-6 text-zinc-500 dark:text-zinc-400 font-light leading-relaxed max-w-sm transition-colors">
            Leveraging cutting-edge artificial intelligence and automation triggers to accelerate development and streamline complex processes.
          </p>
          <div class="hidden lg:block w-12 h-1 bg-zinc-200 dark:bg-zinc-800 mt-8 rounded-full transition-colors"></div>
        </div>
      </div>

      <div class="lg:col-span-8 grid grid-cols-1 sm:grid-cols-2 gap-6 sm:gap-8">
        <div v-for="(tool, index) in aiTools" :key="tool.name" class="opacity-0 flex flex-col items-start p-6 sm:p-8 bg-white dark:bg-zinc-900/50 border border-zinc-200/60 dark:border-zinc-800 rounded-3xl shadow-sm hover:shadow-xl hover:shadow-zinc-200/50 dark:hover:shadow-zinc-900/50 hover:border-zinc-300 dark:hover:border-zinc-700 hover:-translate-y-1.5 transition-all duration-500 cursor-default group" :class="{ 'animate-slide-up': isVisible }" :style="{ animationDelay: `${index * 150 + 150}ms` }">
          
          <div class="mb-6 p-4 rounded-2xl bg-zinc-50 dark:bg-zinc-800/80 border border-zinc-100/80 dark:border-zinc-700/50 group-hover:bg-blue-50 dark:group-hover:bg-zinc-800 group-hover:border-blue-100 dark:group-hover:border-zinc-600 transition-colors duration-500 shadow-sm">
            <!-- dark:invert trick again! -->
            <img :src="`https://cdn.simpleicons.org/${tool.icon}/52525b`" class="w-7 h-7 opacity-70 group-hover:opacity-100 dark:invert dark:opacity-80 transition-all duration-300" :alt="tool.name" />
          </div>
          
          <div>
            <h4 class="text-xl font-bold text-zinc-900 dark:text-white mb-2 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors">{{ tool.name }}</h4>
            <p class="text-zinc-500 dark:text-zinc-400 text-sm sm:text-base font-light leading-relaxed transition-colors">{{ tool.description }}</p>
          </div>
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