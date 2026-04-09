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
    title: 'Master IT Company',
    type: 'Business Website',
    description: 'A sleek, modern website built with WordPress and Elementor, showcasing the company’s services and portfolio with a clean, responsive design.',
    tags: ['WordPress', 'Elementor'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773715509/copy_of_screenshot_2025-07-23_165811_pt6bxi_5820c2.png"
  },
  {
    title: 'Master IT Products',
    type: 'Business Website',
    description: 'Service website for the products of Master IT company that built with WordPress and Elementor, showcasing the company’s services.',
    tags: ['WordPress', 'Elementor'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773715615/copy_of_screenshot_2025-07-23_170447_ltlluf_0a641a.png"
  },
  {
    title: 'Explore Koh Rong',
    type: 'Business Website',
    description: 'Booking Hotel, Rental Car, Tuk Tuk, and Tours for tourists to explore the island seamlessly.',
    tags: ['WordPress', 'Elementor'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773714470/Screenshot_2026-03-17_092725_iigyuh.png"
  },
  {
    title: 'Local Business Tool',
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
  {
    title: 'ERP RPA System',
    type: 'Automation Tool',
    description: 'A powerful tool for automatic data entry and auto process download.',
    tags: ['Vue.js', 'Vuetify', 'Python', 'Django'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773737767/Screenshot_2026-03-17_155539_igvilo.png"
  },
  {
    title: 'DSV RPA System',
    type: 'Automation Tool',
    description: 'A powerful tool for automatic data entry and auto process download invoice from DSV forwarder company.',
    tags: ['Vue.js', 'Tailwind CSS', 'Python', 'Django'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773738140/Screenshot_2026-03-17_160144_ksipef.png"
  },
  {
    title: 'PO Auto Integration',
    type: 'Automation Tool',
    description: 'A powerful tool for automatic data integration from the PO data to the system for the company.',
    tags: ['Vue.js', 'Vuetify', 'TypeScript', 'Django'],
    link: '#',
    img: "https://res.cloudinary.com/dvljcimlz/image/upload/v1773737585/Screenshot_2026-03-17_155218_rkbmhc.png"
  },
]
</script>

<template>
  <section id="projects" class="scroll-mt-24 sm:scroll-mt-32 transition-colors duration-500" ref="portfolioSection">

    <!-- Section Header with Animation & Dark Mode Support -->
    <div 
      class="mb-12 sm:mb-16 opacity-0" 
      :class="{ 'animate-slide-up': isVisible }" 
      style="animation-delay: 0ms;"
    >
      <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-2 sm:mb-3">Selected Work</h2>
      <h3 class="text-3xl sm:text-4xl font-extrabold text-zinc-900 dark:text-white tracking-tight transition-colors">Featured Projects.</h3>
    </div>

    <!-- Projects Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 sm:gap-10">
      <a 
        v-for="(project, index) in projects" 
        :key="index" 
        :href="project.link" 
        target="_blank"
        class="group relative flex flex-col h-[400px] sm:h-[450px] w-full rounded-[2rem] bg-zinc-100 dark:bg-zinc-900 shadow-md hover:shadow-2xl hover:shadow-blue-500/10 dark:hover:shadow-blue-500/5 overflow-hidden transition-all duration-500 hover:-translate-y-2 opacity-0"
        :class="{ 'animate-slide-up': isVisible }" 
        :style="{ animationDelay: `${(index % 3) * 150 + 150}ms` }"
      >
        
        <!-- Background Image Area (Edge-to-Edge) -->
        <div class="absolute inset-0 w-full h-full">
          <!-- Fallback Icon if no image -->
          <div v-if="!project.img || project.img === 'null'" class="w-full h-full flex items-center justify-center bg-zinc-200 dark:bg-zinc-800 text-zinc-400 dark:text-zinc-600 transition-colors">
            <svg class="w-16 h-16 group-hover:scale-110 transition-transform duration-700 ease-out" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
            </svg>
          </div>
          <!-- Actual Project Image -->
          <img v-else :src="project.img" :alt="project.title" class="w-full h-full object-cover object-top group-hover:scale-110 transition-transform duration-700 ease-in-out">
        </div>

        <!-- Gradient Overlay (Always dark so white text remains readable in light AND dark mode) -->
        <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/20 to-transparent opacity-80 group-hover:opacity-95 transition-opacity duration-500 z-10"></div>

        <!-- Top Right Action Button (Diagonal Arrow) -->
        <div class="absolute top-6 right-6 z-20 opacity-0 group-hover:opacity-100 transition-all duration-500 -translate-y-4 group-hover:translate-y-0">
          <div class="bg-white/20 backdrop-blur-md p-3 rounded-full text-white border border-white/20 hover:bg-white hover:text-zinc-900 transition-colors shadow-lg">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"></path>
            </svg>
          </div>
        </div>

        <!-- Typography & Content Overlay -->
        <div class="absolute inset-x-0 bottom-0 p-6 sm:p-8 z-20 flex flex-col justify-end">
          
          <p class="text-[10px] sm:text-xs font-bold text-blue-400 uppercase tracking-widest mb-2">{{ project.type }}</p>
          <h4 class="text-2xl sm:text-3xl font-bold text-white leading-snug drop-shadow-md">
            {{ project.title }}
          </h4>
          
          <!-- Expandable Content Area using CSS Grid trick for smooth height transition -->
          <div class="grid transition-all duration-500 ease-in-out grid-rows-[0fr] group-hover:grid-rows-[1fr] mt-0 group-hover:mt-4">
            <div class="overflow-hidden">
              
              <!-- Description -->
              <p class="text-zinc-300 text-sm sm:text-base font-light leading-relaxed mb-5 line-clamp-2 opacity-0 group-hover:opacity-100 transition-opacity duration-500 delay-150">
                {{ project.description }}
              </p>

              <!-- Tags -->
              <div class="flex flex-wrap gap-2 opacity-0 group-hover:opacity-100 transition-opacity duration-500 delay-200">
                <span v-for="tag in project.tags" :key="tag"
                  class="text-[10px] sm:text-xs font-medium text-white bg-white/10 backdrop-blur-md border border-white/10 px-3 py-1.5 rounded-full tracking-wide">
                  {{ tag }}
                </span>
              </div>

            </div>
          </div>

        </div>

      </a>
    </div>
  </section>
</template>

<style scoped>
/* Custom Keyframe animation for the initial slide-up fade effect */
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
  animation: slideUpFade 0.7s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>