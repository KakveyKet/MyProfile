<script setup>
import { ref, onMounted } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Timeline from './components/Timeline.vue'
import Portfolio from './components/Portfolio.vue'
import Pricing from './components/Pricing.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
import AIStack from './components/AIStack.vue'

// --- Auto-Typing Background Logic ---
const typingSnippets = ref([
  { id: 1, top: '12%', left: '4%', text: '', fullText: '<nav class="flex items-center">\n  <ul class="flex gap-4">\n    <li>Home</li>\n    <li>About</li>\n  </ul>\n</nav>', index: 0, speed: 40 },
  { id: 2, top: '25%', left: '68%', text: '', fullText: 'async function fetchData() {\n  const res = await api.get("/user");\n  return res.data;\n}', index: 0, speed: 30 },
  { id: 3, top: '55%', left: '8%', text: '', fullText: '.glass-effect {\n  backdrop-filter: blur(12px);\n  background: rgba(255,255,255,0.1);\n}', index: 0, speed: 50 },
  { id: 4, top: '65%', left: '72%', text: '', fullText: '<script setup>\nimport { ref } from "vue"\nconst active = ref(true)\n</sc' + 'ript>', index: 0, speed: 45 },
  { id: 5, top: '85%', left: '15%', text: '', fullText: 'class UserProfile(models.Model):\n    user = models.OneToOneField(User)\n    bio = models.TextField()', index: 0, speed: 35 }
])

onMounted(() => {
  typingSnippets.value.forEach((snippet) => {
    const type = () => {
      if (snippet.index < snippet.fullText.length) {
        snippet.text += snippet.fullText.charAt(snippet.index);
        snippet.index++;
        setTimeout(type, snippet.speed);
      } else {
        setTimeout(() => {
          snippet.text = '';
          snippet.index = 0;
          type();
        }, 5000 + Math.random() * 5000);
      }
    };
    setTimeout(type, Math.random() * 3000);
  });
})
</script>

<template>
  <div
    class="relative min-h-screen text-slate-900 dark:text-slate-100 font-sans selection:bg-fuchsia-200 dark:selection:bg-fuchsia-900 selection:text-fuchsia-900 dark:selection:text-fuchsia-100 overflow-hidden transition-colors duration-500">

    <!-- Base Layer: Dotted Developer Grid (Adapts to Dark Mode) -->
    <div
      class="fixed inset-0 z-[-2] bg-slate-50 dark:bg-zinc-950 bg-dot-pattern pointer-events-none transition-colors duration-500">
    </div>

    <!-- Middle Layer: Vibrant Aurora Animated Background -->
    <div class="fixed inset-0 z-[-1] pointer-events-none">
      <div
        class="absolute top-[-10%] left-[-10%] w-[500px] h-[500px] bg-fuchsia-400/30 dark:bg-fuchsia-500/20 rounded-full mix-blend-multiply dark:mix-blend-screen filter blur-[120px] animate-blob transition-colors duration-500">
      </div>
      <div
        class="absolute top-[20%] right-[-10%] w-[400px] h-[400px] bg-cyan-400/30 dark:bg-cyan-500/20 rounded-full mix-blend-multiply dark:mix-blend-screen filter blur-[120px] animate-blob animation-delay-2000 transition-colors duration-500">
      </div>
      <div
        class="absolute bottom-[-20%] left-[20%] w-[600px] h-[600px] bg-violet-400/30 dark:bg-violet-500/20 rounded-full mix-blend-multiply dark:mix-blend-screen filter blur-[120px] animate-blob animation-delay-4000 transition-colors duration-500">
      </div>

      <!-- Auto Typing Code Snippets -->
      <div v-for="snippet in typingSnippets" :key="snippet.id"
        class="absolute text-slate-500/40 dark:text-slate-400/20 font-mono text-[10px] sm:text-xs whitespace-pre select-none drop-shadow-sm transition-colors duration-500"
        :style="{ top: snippet.top, left: snippet.left }">
        {{ snippet.text }}<span class="animate-pulse text-slate-500/50 dark:text-slate-400/40">|</span>
      </div>
    </div>

    <Navbar />

    <main class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12 py-12 space-y-40 relative z-10">
      <Hero />
      <About />
      <Skills />
      <AIStack />
      <Timeline />
      <Portfolio />
      <Pricing />
      <Contact />
    </main>

    <Footer />
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
}

body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Light mode dot pattern */
.bg-dot-pattern {
  background-image: radial-gradient(rgba(15, 23, 42, 0.08) 1px, transparent 1px);
  background-size: 24px 24px;
}

/* Dark mode dot pattern */
.dark .bg-dot-pattern {
  background-image: radial-gradient(rgba(255, 255, 255, 0.08) 1px, transparent 1px);
}

@keyframes blob {
  0% {
    transform: translate(0px, 0px) scale(1);
  }

  33% {
    transform: translate(40px, -50px) scale(1.1);
  }

  66% {
    transform: translate(-30px, 30px) scale(0.9);
  }

  100% {
    transform: translate(0px, 0px) scale(1);
  }
}

.animate-blob {
  animation: blob 20s infinite alternate ease-in-out;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

.animation-delay-4000 {
  animation-delay: 4s;
}
</style>