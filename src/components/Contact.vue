<script setup>
import { ref, onMounted } from 'vue'

// 1. Setup Intersection Observer for scroll animations
const contactSection = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      observer.disconnect()
    }
  }, {
    threshold: 0.1
  })

  if (contactSection.value) {
    observer.observe(contactSection.value)
  }
})

// 2. Updated Contact Info
const contactInfo = [
  { label: 'Email', value: 'kakveyket408@gmail.com' },
  { label: 'Phone', value: '+855 96 763 609' },
  { label: 'Telegram', value: '@VKak_vey' },
]

// 3. Updated Socials with links
const socials = [
  { name: 'GitHub', href: 'https://github.com/KakveyKet' },
  { name: 'LinkedIn', href: 'https://www.linkedin.com/in/kakvey-ket-b22203364' },
  { name: 'Facebook', href: 'https://www.facebook.com/profile.php?id=61584525802922' },
  { name: "Youtube", href: 'https://www.youtube.com/@KakveyKet' },
]
</script>

<template>
  <section id="contact" class="scroll-mt-24 sm:scroll-mt-32 pb-10 sm:pb-20" ref="contactSection">
    
    <div 
      class="bg-zinc-900 rounded-[2rem] sm:rounded-[2.5rem] overflow-hidden flex flex-col lg:flex-row text-zinc-100 shadow-2xl opacity-0"
      :class="{ 'animate-slide-up': isVisible }"
    >
      
      <!-- Info Pane (Dark) -->
      <div class="lg:w-2/5 p-8 sm:p-12 lg:p-16 flex flex-col justify-between border-b lg:border-b-0 lg:border-r border-zinc-800 relative overflow-hidden">
        
        <!-- Modern decorative glow effect -->
        <div class="absolute -bottom-32 -left-32 w-64 h-64 bg-blue-600 rounded-full mix-blend-screen filter blur-[100px] opacity-30"></div>

        <div class="relative z-10">
          <h2 class="text-3xl sm:text-4xl font-bold mb-4 text-white tracking-tight">Let's build something.</h2>
          <p class="text-zinc-400 font-light text-base sm:text-lg mb-10 sm:mb-12 max-w-sm leading-relaxed">
            Have a project in mind? Reach out and let's discuss how I can help your business grow.
          </p>
          
          <div class="space-y-8">
            <div v-for="info in contactInfo" :key="info.label" class="group cursor-pointer">
              <p class="text-xs font-semibold text-zinc-500 uppercase tracking-widest mb-1">{{ info.label }}</p>
              <div class="text-lg sm:text-xl font-medium text-zinc-100 relative overflow-hidden inline-flex">
                <span class="block transition-transform duration-300 group-hover:-translate-y-full">{{ info.value }}</span>
                <span class="block absolute inset-0 transition-transform duration-300 translate-y-full group-hover:translate-y-0 text-blue-400">{{ info.value }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Social Links -->
        <div class="mt-16 sm:mt-20 flex flex-wrap gap-4 sm:gap-6 relative z-10">
          <a 
            v-for="social in socials" 
            :key="social.name" 
            :href="social.href" 
            target="_blank"
            class="text-sm font-medium text-zinc-400 hover:text-white transition-colors py-1 relative after:absolute after:bottom-0 after:left-0 after:h-[2px] after:w-0 after:bg-white after:transition-all hover:after:w-full"
          >
            {{ social.name }}
          </a>
        </div>
      </div>

      <!-- Form Pane (Light) -->
      <div class="lg:w-3/5 p-8 sm:p-12 lg:p-16 bg-white text-zinc-900 relative">
        <form class="space-y-8 sm:space-y-10" @submit.prevent>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8 sm:gap-10">
            <!-- Name Input -->
            <div class="relative">
              <input type="text" id="name" class="peer w-full border-b-2 border-zinc-200 py-2.5 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent text-lg font-medium" placeholder="Name">
              <label for="name" class="absolute left-0 -top-4 text-xs font-bold text-zinc-400 uppercase tracking-wider transition-all peer-placeholder-shown:text-base peer-placeholder-shown:font-normal peer-placeholder-shown:text-zinc-500 peer-placeholder-shown:top-2.5 peer-focus:-top-4 peer-focus:text-xs peer-focus:font-bold peer-focus:text-zinc-900 cursor-text">
                Name
              </label>
            </div>
            
            <!-- Email Input -->
            <div class="relative">
              <input type="email" id="email" class="peer w-full border-b-2 border-zinc-200 py-2.5 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent text-lg font-medium" placeholder="Email">
              <label for="email" class="absolute left-0 -top-4 text-xs font-bold text-zinc-400 uppercase tracking-wider transition-all peer-placeholder-shown:text-base peer-placeholder-shown:font-normal peer-placeholder-shown:text-zinc-500 peer-placeholder-shown:top-2.5 peer-focus:-top-4 peer-focus:text-xs peer-focus:font-bold peer-focus:text-zinc-900 cursor-text">
                Email Address
              </label>
            </div>
          </div>
          
          <!-- Subject Input -->
          <div class="relative">
            <input type="text" id="subject" class="peer w-full border-b-2 border-zinc-200 py-2.5 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent text-lg font-medium" placeholder="Subject">
            <label for="subject" class="absolute left-0 -top-4 text-xs font-bold text-zinc-400 uppercase tracking-wider transition-all peer-placeholder-shown:text-base peer-placeholder-shown:font-normal peer-placeholder-shown:text-zinc-500 peer-placeholder-shown:top-2.5 peer-focus:-top-4 peer-focus:text-xs peer-focus:font-bold peer-focus:text-zinc-900 cursor-text">
              Subject
            </label>
          </div>
          
          <!-- Message Textarea -->
          <div class="relative mt-12">
            <textarea id="message" rows="4" class="peer w-full border-b-2 border-zinc-200 py-2.5 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent resize-none text-lg font-medium" placeholder="Project Details"></textarea>
            <label for="message" class="absolute left-0 -top-4 text-xs font-bold text-zinc-400 uppercase tracking-wider transition-all peer-placeholder-shown:text-base peer-placeholder-shown:font-normal peer-placeholder-shown:text-zinc-500 peer-placeholder-shown:top-2.5 peer-focus:-top-4 peer-focus:text-xs peer-focus:font-bold peer-focus:text-zinc-900 cursor-text">
              Project Details
            </label>
          </div>
          
          <div class="pt-6 sm:pt-8">
            <button type="submit" class="w-full sm:w-auto px-10 py-4 bg-zinc-900 text-white text-sm font-bold uppercase tracking-widest rounded-full hover:bg-blue-600 transition-colors duration-300 flex items-center justify-center shadow-lg hover:shadow-xl hover:-translate-y-1">
              Send Message
              <svg class="w-5 h-5 ml-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
              </svg>
            </button>
          </div>
          
        </form>
      </div>
      
    </div>
  </section>
</template>

<style scoped>
/* Custom Keyframe animation for the slide-up fade effect */
@keyframes slideUpFade {
  from {
    opacity: 0;
    transform: translateY(40px) scale(0.98);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-slide-up {
  animation: slideUpFade 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

/* Custom easing for the flip text animation */
.group:hover span.block {
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}
</style>