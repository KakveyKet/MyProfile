<script setup>
import { ref, onMounted } from 'vue'
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Skills from './components/Skills.vue'
import Timeline from './components/Timeline.vue'
import Portfolio from './components/Portfolio.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
import AIStack from './components/AIStack.vue'

// --- Auto-Typing Background Logic ---
const typingSnippets = ref([
  {
    id: 1,
    top: '12%',
    left: '4%',
    text: '',
    fullText: '<nav class="flex items-center">\n  <ul class="flex gap-4">\n    <li>Home</li>\n    <li>About</li>\n  </ul>\n</nav>',
    index: 0,
    speed: 40 // ms per char
  },
  {
    id: 2,
    top: '25%',
    left: '68%',
    text: '',
    fullText: 'async function fetchData() {\n  const res = await api.get("/user");\n  return res.data;\n}',
    index: 0,
    speed: 30
  },
  {
    id: 3,
    top: '55%',
    left: '8%',
    text: '',
    fullText: '.glass-effect {\n  backdrop-filter: blur(12px);\n  background: rgba(255,255,255,0.1);\n}',
    index: 0,
    speed: 50
  },
  {
    id: 4,
    top: '65%',
    left: '72%',
    text: '',
    fullText: '<script setup>\nimport { ref } from "vue"\nconst active = ref(true)\n</sc' + 'ript>',
    index: 0,
    speed: 45
  },
  {
    id: 5,
    top: '85%',
    left: '15%',
    text: '',
    fullText: 'class UserProfile(models.Model):\n    user = models.OneToOneField(User)\n    bio = models.TextField()',
    index: 0,
    speed: 35
  }
])

onMounted(() => {
  typingSnippets.value.forEach((snippet) => {
    const type = () => {
      if (snippet.index < snippet.fullText.length) {
        snippet.text += snippet.fullText.charAt(snippet.index);
        snippet.index++;
        setTimeout(type, snippet.speed);
      } else {
        // Wait a few seconds after finishing, then clear and restart
        setTimeout(() => {
          snippet.text = '';
          snippet.index = 0;
          type();
        }, 5000 + Math.random() * 5000); 
      }
    };
    // Start each snippet with a random delay so they don't all start at once
    setTimeout(type, Math.random() * 3000);
  });
})
</script>

<template>
  <div class="relative min-h-screen text-slate-900 font-sans selection:bg-fuchsia-200 selection:text-fuchsia-900 overflow-hidden">
    
    <!-- Base Layer: Dotted Developer Grid -->
    <div class="fixed inset-0 z-[-2] bg-slate-50 bg-dot-pattern pointer-events-none"></div>

    <!-- Middle Layer: Vibrant Aurora Animated Background -->
    <div class="fixed inset-0 z-[-1] pointer-events-none">
      
      <!-- Glowing Glassmorphism Blobs with richer colors -->
      <div class="absolute top-[-10%] left-[-10%] w-[500px] h-[500px] bg-fuchsia-400/30 rounded-full mix-blend-multiply filter blur-[120px] animate-blob"></div>
      <div class="absolute top-[20%] right-[-10%] w-[400px] h-[400px] bg-cyan-400/30 rounded-full mix-blend-multiply filter blur-[120px] animate-blob animation-delay-2000"></div>
      <div class="absolute bottom-[-20%] left-[20%] w-[600px] h-[600px] bg-violet-400/30 rounded-full mix-blend-multiply filter blur-[120px] animate-blob animation-delay-4000"></div>

      <!-- Auto Typing Code Snippets -->
      <div
        v-for="snippet in typingSnippets"
        :key="snippet.id"
        class="absolute text-slate-500/30 font-mono text-[10px] sm:text-xs whitespace-pre select-none drop-shadow-sm"
        :style="{ top: snippet.top, left: snippet.left }"
      >
        {{ snippet.text }}<span class="animate-pulse text-slate-500/50">|</span>
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

/* Dotted background pattern for that premium tech feel */
.bg-dot-pattern {
  background-image: radial-gradient(rgba(15, 23, 42, 0.08) 1px, transparent 1px);
  background-size: 24px 24px;
}

/* Custom Animation Keyframes for the blobs */
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