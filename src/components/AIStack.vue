<script setup>
import { ref, onMounted } from 'vue'

// 1. Setup Intersection Observer for scroll animations
const aiSection = ref(null)
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

  if (aiSection.value) {
    observer.observe(aiSection.value)
  }
})

// 2. AI Tools Data with corresponding simpleicon slugs
const aiTools = [
  { 
    name: 'ChatGPT', 
    icon: 'dependabot', 
    description: 'Advanced reasoning, problem-solving, and code architecture assistance.' 
  },
  { 
    name: 'Gemini', 
    icon: 'googlegemini', 
    description: 'Multimodal analysis and deep integration with Google ecosystems.' 
  },
  { 
    name: 'Grok', 
    icon: 'x', // Using X logo as Grok is by xAI
    description: 'Real-time data synthesis and rapid problem solving.' 
  },
  { 
    name: 'Copilot', 
    icon: 'githubcopilot', 
    description: 'In-IDE contextual code generation and intelligent auto-completion.' 
  },
  { 
    name: 'Webhooks', 
    icon: 'jsonwebtokens', 
    description: 'Automated cross-platform triggers connecting AI to external services.' 
  }
]
</script>

<template>
  <section id="ai-stack" class="scroll-mt-24 sm:scroll-mt-32" ref="aiSection">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-16 items-start">
      
      <!-- Left Column: Section Header (Sticky on Desktop) -->
      <div class="lg:col-span-4 lg:sticky lg:top-32 relative">
        <div 
          class="opacity-0"
          :class="{ 'animate-slide-up': isVisible }"
          style="animation-delay: 0ms;"
        >
          <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Workflow</h2>
          <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 tracking-tight">AI Stack.</h3>
          
          <p class="mt-6 text-zinc-500 font-light leading-relaxed max-w-sm">
            Leveraging cutting-edge artificial intelligence and automation triggers to accelerate development and streamline complex processes.
          </p>
          
          <!-- Decorative subtle line -->
          <div class="hidden lg:block w-12 h-1 bg-zinc-200 mt-8 rounded-full"></div>
        </div>
      </div>

      <!-- Right Column: AI Tools Grid -->
      <div class="lg:col-span-8 grid grid-cols-1 sm:grid-cols-2 gap-6 sm:gap-8">
        <div 
          v-for="(tool, index) in aiTools" 
          :key="tool.name"
          class="opacity-0 flex flex-col items-start p-6 sm:p-8 bg-white border border-zinc-200/60 rounded-3xl shadow-sm hover:shadow-xl hover:shadow-zinc-200/50 hover:border-zinc-300 hover:-translate-y-1.5 transition-all duration-500 cursor-default group"
          :class="{ 'animate-slide-up': isVisible }"
          :style="{ animationDelay: `${index * 150 + 150}ms` }"
        >
          <!-- Premium Icon Box -->
          <div class="mb-6 p-4 rounded-2xl bg-zinc-50 border border-zinc-100/80 group-hover:bg-blue-50 group-hover:border-blue-100 transition-colors duration-500 shadow-sm">
            <!-- Pulls the SVG icon from simpleicons.org colored to zinc-600 (52525b) -->
            <img :src="`https://cdn.simpleicons.org/${tool.icon}/52525b`" class="w-7 h-7 opacity-70 group-hover:opacity-100 transition-opacity duration-300" :alt="tool.name" />
          </div>
          
          <!-- Details -->
          <div>
            <h4 class="text-xl font-bold text-zinc-900 mb-2 group-hover:text-blue-600 transition-colors">{{ tool.name }}</h4>
            <p class="text-zinc-500 text-sm sm:text-base font-light leading-relaxed">{{ tool.description }}</p>
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