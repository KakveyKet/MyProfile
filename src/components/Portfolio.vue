<script setup>
import { ref, onMounted } from 'vue'

// 1. Setup Intersection Observer for scroll animations
const portfolioSection = ref(null)
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

  if (portfolioSection.value) {
    observer.observe(portfolioSection.value)
  }
})

// 2. Projects Data
const projects = [
  {
    title: 'E-Commerce Platform',
    type: 'Web Application',
    description: 'A high-performance storefront built with Vue 3, Firebase, and Tailwind CSS, featuring a custom shopping cart and real-time inventory management.',
    tags: ['Vue.js', 'Tailwind', 'Firebase'],
    link: 'https://nubbemart.vercel.app/',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773716050/copy_of_screenshot_2025-07-23_165539_pm0acy_7c107b.png"
  },
  {
    title: 'School Management System',
    type: 'Web Application',
    description: 'A robust Python & Django tool designed to automatically parse, split, and process enterprise invoices, eliminating manual data entry.',
    tags: ['Vue.js', 'Express', 'Tailwind CSS', 'MongoDB'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1753265313/Screenshot_2025-07-23_170739_y2xp0b.png"
  },
  {
    title: 'Master IT Company Website',
    type: 'Business Website',
    description: 'A sleek, modern website built with WordPress and Elementor, showcasing the company’s services and portfolio with a clean, responsive design.',
    tags: ['WordPress', 'Elementor'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773715509/copy_of_screenshot_2025-07-23_165811_pt6bxi_5820c2.png"
  },
  {
    title: 'Master IT Product Website',
    type: 'Business Website',
    description: 'Service website for the products of Master IT company that built with WordPress and Elementor, showcasing the company’s services.',
    tags: ['WordPress', 'Elementor'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773715615/copy_of_screenshot_2025-07-23_170447_ltlluf_0a641a.png"
  },
  {
    title: 'Explore Koh Rong Website',
    type: 'Business Website',
    description: 'Booking Hotel, Rental Car, Tuk Tuk, and Tours for tourists to explore the island seamlessly.',
    tags: ['WordPress', 'Elementor'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773714470/Screenshot_2026-03-17_092725_iigyuh.png"
  },
  {
    title: 'Local Business Website',
    type: 'Business Website',
    description: 'Sell Local Products and also provide services for the local business with automated workflows.',
    tags: ['Glide App', 'Webhook'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773715112/Screenshot_2026-03-17_093819_uidoms.png"
  },
   {
    title: 'Digital Content',
    type: 'Digital Marketing',
    description: 'Post and Advice about the web development and also the technology to the Facebook page to help the people who want to learn about web development and technology.',
    tags: ['Facebook', 'Telegram', 'YouTube'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773718409/copy_of_photo_2026-03-17_10-31-32_pceeus_5f53ad.jpg"
  },
]
</script>

<template>
  <section id="projects" class="scroll-mt-32" ref="portfolioSection">
    
    <!-- Section Header with Animation -->
    <div 
      class="mb-16 opacity-0"
      :class="{ 'animate-slide-up': isVisible }"
      style="animation-delay: 0ms;"
    >
      <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Selected Work</h2>
      <h3 class="text-3xl font-bold text-zinc-900">Featured Projects.</h3>
    </div>

    <!-- Projects Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <a 
        v-for="(project, index) in projects" 
        :key="index" 
        :href="project.link" 
        target="_blank"
        class="group flex flex-col h-full bg-white rounded-2xl shadow-sm hover:shadow-xl border border-zinc-200/60 overflow-hidden hover:-translate-y-2 transition-all duration-300 opacity-0"
        :class="{ 'animate-slide-up': isVisible }"
        :style="{ animationDelay: `${index * 150 + 150}ms` }"
      >
        <!-- Image Area -->
        <div class="h-56 bg-zinc-100 relative overflow-hidden border-b border-zinc-100">
          <!-- Dark overlay on hover -->
          <div class="absolute inset-0 bg-zinc-900/0 group-hover:bg-zinc-900/10 transition-colors duration-300 z-10"></div>
          
          <div class="w-full h-full flex items-center justify-center text-zinc-300 bg-zinc-50">
            <!-- Fallback Icon if no image -->
            <svg v-if="!project.img || project.img === 'null'" class="w-10 h-10 group-hover:scale-110 transition-transform duration-500"
              fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5"
                d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z">
              </path>
            </svg>
            <!-- Actual Project Image -->
            <img v-else :src="project.img" :alt="project.title"
              class="w-full h-full object-cover object-top group-hover:scale-105 transition-transform duration-700 ease-out">
          </div>
        </div>

        <!-- Typography & Content -->
        <div class="p-6 flex-1 flex flex-col">
          <p class="text-xs font-bold text-zinc-400 uppercase tracking-wider mb-2">{{ project.type }}</p>
          <h4 class="text-xl font-bold text-zinc-900 mb-3 group-hover:text-blue-600 transition-colors line-clamp-2">
            {{ project.title }}
          </h4>
          <p class="text-zinc-500 text-sm font-light mb-6 flex-1 line-clamp-3">
            {{ project.description }}
          </p>

          <!-- Tags -->
          <div class="flex flex-wrap gap-2 mt-auto pt-4 border-t border-zinc-50">
            <span v-for="tag in project.tags" :key="tag"
              class="text-xs font-medium text-zinc-600 bg-zinc-100 border border-zinc-200/60 px-2.5 py-1 rounded-md">
              {{ tag }}
            </span>
          </div>
        </div>
      </a>
    </div>
  </section>
</template>

<style scoped>
/* Custom Keyframe animation for the slide-up fade effect */
@keyframes slideUpFade {
  from {
    opacity: 0;
    transform: translateY(30px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.animate-slide-up {
  animation: slideUpFade 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>