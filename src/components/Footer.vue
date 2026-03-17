<script setup>
const contactLinks = [
  { name: 'kakveyket408@gmail.com', href: 'mailto:kakveyket408@gmail.com' },
  { name: '+855 96 763 609', href: 'tel:+85596763609' }
]

const socialLinks = [
  { name: 'Telegram', href: 'https://t.me/VKak_vey' },
  { name: 'Facebook', href: 'https://www.facebook.com/profile.php?id=61584525802922' },
  { name: 'LinkedIn', href: 'https://www.linkedin.com/in/kakvey-ket-b22203364' },
  { name: 'GitHub', href: 'https://github.com/KakveyKet' },
  { name: 'YouTube', href: 'https://www.youtube.com/@KakveyKet' }
]
</script>

<template>
  <footer class="bg-zinc-50 text-zinc-500 pt-16 pb-8 border-t border-zinc-200">
    <div class="max-w-6xl mx-auto px-6 sm:px-8 lg:px-12">
      
      <!-- Top Section: Brand & Links Grid -->
      <div class="grid grid-cols-1 md:grid-cols-12 gap-12 md:gap-8 mb-16">
        
        <!-- Brand Info -->
        <div class="md:col-span-6 lg:col-span-5">
          <a href="#" class="inline-block text-2xl font-bold tracking-tighter text-zinc-900 mb-4">
            Kakvey<span class="text-zinc-400">.DEV</span>
          </a>
          <p class="text-zinc-500 font-light leading-relaxed max-w-sm">
            A Full Stack Web Developer focused on building high-performance web applications, automated workflows, and modern digital experiences.
          </p>
        </div>

        <!-- Contact & Social Columns -->
        <div class="md:col-span-6 lg:col-span-7 grid grid-cols-1 sm:grid-cols-2 gap-10 sm:gap-8">
          
          <!-- Direct Contact -->
          <div>
            <h4 class="text-xs font-bold text-zinc-900 uppercase tracking-widest mb-6">Get in Touch</h4>
            <ul class="space-y-4">
              <li v-for="link in contactLinks" :key="link.name">
                <a :href="link.href" class="text-sm font-medium hover:text-blue-600 transition-colors duration-300 flex items-center group">
                  <span class="relative overflow-hidden">
                    <span class="block transition-transform duration-300 group-hover:-translate-y-full">{{ link.name }}</span>
                    <span class="block absolute inset-0 transition-transform duration-300 translate-y-full group-hover:translate-y-0 text-blue-600">{{ link.name }}</span>
                  </span>
                </a>
              </li>
            </ul>
          </div>

          <!-- Social Platforms -->
          <div>
            <h4 class="text-xs font-bold text-zinc-900 uppercase tracking-widest mb-6">Socials</h4>
            <ul class="space-y-4">
              <li v-for="link in socialLinks" :key="link.name">
                <a :href="link.href" target="_blank" rel="noopener noreferrer" class="text-sm font-medium hover:text-blue-600 transition-colors duration-300 inline-flex items-center">
                  {{ link.name }}
                  <svg class="w-3 h-3 ml-1.5 opacity-0 -translate-y-1 -translate-x-1 group-hover:opacity-100 group-hover:translate-y-0 group-hover:translate-x-0 transition-all duration-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
                  </svg>
                </a>
              </li>
            </ul>
          </div>

        </div>
      </div>

      <!-- Bottom Section: Copyright & Legal -->
      <div class="flex flex-col md:flex-row justify-between items-center pt-8 border-t border-zinc-200 gap-4 md:gap-0">
        <p class="text-sm font-medium text-center md:text-left">
          © {{ new Date().getFullYear() }} Kakvey.DEV. All rights reserved.
        </p>
        <div class="flex flex-wrap justify-center gap-x-6 gap-y-2 text-sm font-medium">
          <a href="#" class="hover:text-zinc-900 transition-colors py-1">Privacy Policy</a>
          <a href="#" class="hover:text-zinc-900 transition-colors py-1">Terms of Service</a>
        </div>
      </div>

    </div>
  </footer>
</template>

<style scoped>
/* Added scoped styles specifically for the link hover animations */
a.group:hover span span {
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}
</style>