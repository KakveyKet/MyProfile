<script setup>
// REPLACE THIS URL WITH YOUR ACTUAL PROFESSIONAL HEADSHOT
// You can upload your photo to Cloudinary (like your project images) and paste the link here.
const profileImage = "https://res.cloudinary.com/dvljcimlz/image/upload/v1775697459/Brown_Classy_Men_Facebook_Profile_Picture_yurhoh.png"
</script>

<template>
  <section id="hero" class="pt-24 sm:pt-32 pb-16 min-h-[85vh] flex items-center">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-center w-full">
      
      <!-- Left Column: Content -->
      <div class="lg:col-span-7 flex flex-col items-start animate-fade-in-up">
        
        <!-- Availability Badge -->
        <div class="inline-flex items-center px-3 sm:px-4 py-1.5 mb-8 rounded-full bg-green-50 border border-green-200/60 text-green-700 text-[10px] sm:text-xs font-bold uppercase tracking-widest shadow-sm">
          <span class="relative flex h-2 w-2 mr-2.5">
            <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-green-400 opacity-75"></span>
            <span class="relative inline-flex rounded-full h-2 w-2 bg-green-500"></span>
          </span>
          Available for new projects
        </div>

        <h1 class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-extrabold tracking-tight text-zinc-900 leading-[1.1] mb-6 sm:mb-8">
          Building elegant <br class="hidden sm:block"/>
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-zinc-400 to-zinc-600">digital solutions.</span>
        </h1>
        
        <p class="text-base sm:text-lg md:text-xl text-zinc-500 max-w-2xl mb-10 sm:mb-12 leading-relaxed font-light">
          I'm a Full Stack Web Developer specializing in scalable architectures, process automation, and high-performance web applications. Turning complex problems into seamless code.
        </p>
        
        <div class="flex flex-col sm:flex-row gap-4 w-full sm:w-auto">
          <a href="#projects" class="inline-flex justify-center items-center px-8 py-4 bg-zinc-900 text-white text-sm font-bold uppercase tracking-widest rounded-full hover:bg-zinc-800 transition-all shadow-lg hover:shadow-xl hover:-translate-y-0.5">
            Explore My Work
          </a>
          <a href="#contact" class="inline-flex justify-center items-center px-8 py-4 bg-white text-zinc-900 text-sm font-bold uppercase tracking-widest rounded-full border border-zinc-200 hover:border-zinc-300 hover:bg-zinc-50 transition-all shadow-sm">
            Contact Me
          </a>
        </div>
      </div>

      <!-- Right Column: Profile Image & Visuals -->
      <div class="lg:col-span-5 relative mt-10 lg:mt-0 animate-fade-in-up" style="animation-delay: 200ms;">
        
        <!-- Abstract Glowing Background Behind Image -->
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[120%] h-[120%] bg-blue-100/50 rounded-full mix-blend-multiply filter blur-[80px] opacity-70 z-0 pointer-events-none"></div>

        <!-- Main Profile Image Container -->
        <div class="relative z-10 w-full aspect-[4/5] sm:aspect-square lg:aspect-[4/5] rounded-[2.5rem] overflow-hidden border border-zinc-200/50 shadow-2xl group bg-zinc-100">
          
          <!-- Image Overlay Gradient (Lightened for portraits) -->
          <div class="absolute inset-0 bg-gradient-to-tr from-zinc-900/20 via-transparent to-transparent z-10 pointer-events-none transition-opacity duration-500 group-hover:opacity-40"></div>
          
          <img 
            :src="profileImage" 
            alt="Kakvey - Full Stack Developer" 
            class="w-full h-full object-cover object-center group-hover:scale-105 transition-transform duration-700 ease-out"
          />
          
        </div>

        <!-- Floating Glassmorphism Badge -->
        <div class="absolute -bottom-6 -left-4 sm:-left-8 z-20 bg-white/90 backdrop-blur-md border border-zinc-200/80 p-4 sm:p-5 rounded-2xl shadow-xl flex items-center gap-4 animate-float">
          <div class="p-3 bg-blue-50 rounded-xl text-blue-600">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"></path>
            </svg>
          </div>
          <div>
            <p class="text-zinc-900 font-bold text-sm sm:text-base">Full Stack</p>
            <p class="text-zinc-500 text-xs sm:text-sm font-medium">Development & Automation</p>
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