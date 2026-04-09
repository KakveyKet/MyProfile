<script setup>
// Your actual professional headshot
const profileImage = "https://res.cloudinary.com/dvljcimlz/image/upload/v1775697459/Brown_Classy_Men_Facebook_Profile_Picture_yurhoh.png"
</script>

<template>
  <section id="hero" class="pt-24 sm:pt-32 pb-16 min-h-[85vh] flex items-center transition-colors duration-500">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-center w-full">
      
      <!-- Left Column: Content -->
      <div class="lg:col-span-7 flex flex-col items-start animate-fade-in-up">
        
        <!-- Availability Badge -->
        <div class="inline-flex items-center px-3 sm:px-4 py-1.5 mb-8 rounded-full bg-green-50 dark:bg-green-500/10 border border-green-200/60 dark:border-green-500/20 text-green-700 dark:text-green-400 text-[10px] sm:text-xs font-bold uppercase tracking-widest shadow-sm transition-colors duration-300">
          <span class="relative flex h-2 w-2 mr-2.5">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
            <span class="relative inline-flex rounded-full h-2 w-2 bg-green-500"></span>
          </span>
          Available for new projects
        </div>

        <!-- Headline -->
        <h1 class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-extrabold tracking-tight text-zinc-900 dark:text-white leading-[1.1] mb-6 sm:mb-8 transition-colors duration-300">
          Building elegant <br class="hidden sm:block"/>
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-zinc-400 to-zinc-600 dark:from-zinc-300 dark:to-zinc-500">digital solutions.</span>
        </h1>
        
        <!-- Subheadline -->
        <p class="text-base sm:text-lg md:text-xl text-zinc-500 dark:text-zinc-400 max-w-2xl mb-10 sm:mb-12 leading-relaxed font-light transition-colors duration-300">
          I'm a Full Stack Web Developer specializing in scalable architectures, process automation, and high-performance web applications. Turning complex problems into seamless code.
        </p>
        
        <!-- CTA Buttons -->
        <div class="flex flex-col sm:flex-row gap-4 w-full sm:w-auto">
          <!-- Primary Button (Inverts on dark mode) -->
          <a href="#projects" class="inline-flex justify-center items-center px-8 py-4 bg-zinc-900 dark:bg-white text-white dark:text-zinc-900 text-sm font-bold uppercase tracking-widest rounded-full hover:bg-zinc-800 dark:hover:bg-zinc-200 transition-all duration-300 shadow-lg hover:shadow-xl hover:-translate-y-0.5">
            Explore My Work
          </a>
          <!-- Secondary Button -->
          <a href="#contact" class="inline-flex justify-center items-center px-8 py-4 bg-white dark:bg-zinc-900/50 text-zinc-900 dark:text-white text-sm font-bold uppercase tracking-widest rounded-full border border-zinc-200 dark:border-zinc-700 hover:border-zinc-300 dark:hover:border-zinc-600 hover:bg-zinc-50 dark:hover:bg-zinc-800 transition-all duration-300 shadow-sm">
            Contact Me
          </a>
        </div>
      </div>

      <!-- Right Column: Profile Image & Visuals -->
      <div class="lg:col-span-5 relative mt-10 lg:mt-0 animate-fade-in-up" style="animation-delay: 200ms;">
        
        <!-- Abstract Glowing Background Behind Image -->
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[120%] h-[120%] bg-blue-100/50 dark:bg-blue-500/20 rounded-full mix-blend-multiply dark:mix-blend-screen filter blur-[80px] opacity-70 z-0 pointer-events-none transition-colors duration-500"></div>

        <!-- Main Profile Image Container -->
        <div class="relative z-10 w-full aspect-[4/5] sm:aspect-square lg:aspect-[4/5] rounded-[2.5rem] overflow-hidden border border-zinc-200/50 dark:border-zinc-700/50 shadow-2xl group bg-zinc-100 dark:bg-zinc-800 transition-colors duration-300">
          
          <!-- Image Overlay Gradient -->
          <div class="absolute inset-0 bg-gradient-to-tr from-zinc-900/10 dark:from-zinc-900/60 via-transparent to-transparent z-10 pointer-events-none transition-opacity duration-500 group-hover:opacity-30 dark:group-hover:opacity-80"></div>
          
          <img 
            :src="profileImage" 
            alt="Kakvey Ket - Full Stack Developer" 
            class="w-full h-full object-cover object-center group-hover:scale-105 transition-transform duration-700 ease-out"
          />
          
        </div>

        <!-- Floating Glassmorphism Badge -->
        <div class="absolute -bottom-6 -left-4 sm:-left-8 z-20 bg-white/90 dark:bg-zinc-900/90 backdrop-blur-md border border-zinc-200/80 dark:border-zinc-700/80 p-4 sm:p-5 rounded-2xl shadow-xl flex items-center gap-4 animate-float transition-colors duration-300">
          <div class="p-3 bg-blue-50 dark:bg-blue-500/20 rounded-xl text-blue-600 dark:text-blue-400 transition-colors duration-300">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path>
            </svg>
          </div>
          <div>
            <p class="text-zinc-900 dark:text-white font-bold text-sm sm:text-base transition-colors duration-300">Full Stack</p>
            <p class="text-zinc-500 dark:text-zinc-400 text-xs sm:text-sm font-medium transition-colors duration-300">Development & Automation</p>
          </div>
        </div>

      </div>

    </div>
  </section>
</template>

<style scoped>
/* Fade in and slide up animation for page load */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in-up {
  opacity: 0;
  animation: fadeInUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

/* Subtle floating animation for the overlapping badge */
@keyframes float {
  0% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
  100% { transform: translateY(0px); }
}

.animate-float {
  animation: float 6s ease-in-out infinite;
}
</style>