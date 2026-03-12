<script setup>
</script>

<template>
  <section id="hero" class="pt-32 pb-16 flex flex-col items-start justify-center min-h-[85vh]">
    <!-- Availability Badge -->
    <div class="inline-flex items-center px-3 py-1 mb-8 rounded-full bg-green-50 border border-green-200/60 text-green-700 text-xs font-semibold uppercase tracking-wider">
      <span class="w-2 h-2 rounded-full bg-green-500 mr-2 animate-pulse"></span>
      Available for new projects
    </div>

    <h1 class="text-5xl md:text-7xl font-extrabold tracking-tight text-zinc-900 leading-[1.1] mb-6">
      Building robust <br class="hidden md:block"/>
      <span class="text-zinc-400">digital solutions.</span>
    </h1>
    
    <p class="text-lg md:text-xl text-zinc-500 max-w-2xl mb-12 leading-relaxed font-light">
      I'm a Full Stack Web Developer specializing in scalable architectures, process automation, and high-performance web applications. Turning complex problems into elegant code.
    </p>
    
    <div class="flex flex-col sm:flex-row gap-4 w-full sm:w-auto">
      <a href="#projects" class="inline-flex justify-center items-center px-8 py-3.5 bg-zinc-900 text-white font-medium rounded-full hover:bg-zinc-800 transition-all shadow-sm hover:shadow-md">
        Explore My Work
      </a>
      <a href="#contact" class="inline-flex justify-center items-center px-8 py-3.5 bg-white text-zinc-900 font-medium rounded-full border border-zinc-200 hover:border-zinc-300 transition-all">
        Contact Me
      </a>
    </div>
  </section>
</template>