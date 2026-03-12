<script setup>
const contactInfo = [
  { label: 'Email', value: 'hello@yourdomain.com' },
  { label: 'Phone', value: '+855 12 345 678' },
  { label: 'Telegram', value: '@yourusername' },
]

const socials = ['GitHub', 'LinkedIn', 'Facebook']
</script>

<template>
  <section id="contact" class="scroll-mt-32 pb-20">
    <div class="bg-zinc-900 rounded-[2.5rem] overflow-hidden flex flex-col lg:flex-row text-zinc-100 shadow-2xl">
      
      <!-- Info Pane -->
      <div class="lg:w-2/5 p-12 lg:p-16 flex flex-col justify-between border-b lg:border-b-0 lg:border-r border-zinc-800">
        <div>
          <h2 class="text-3xl font-bold mb-4 text-white">Let's build something.</h2>
          <p class="text-zinc-400 font-light text-lg mb-12 max-w-sm">Have a project in mind? Reach out and let's discuss how I can help your business grow.</p>
          
          <div class="space-y-6">
            <div v-for="info in contactInfo" :key="info.label">
              <p class="text-xs font-semibold text-zinc-500 uppercase tracking-wider mb-1">{{ info.label }}</p>
              <p class="text-lg font-medium">{{ info.value }}</p>
            </div>
          </div>
        </div>

        <div class="mt-16 flex space-x-6">
          <a v-for="social in socials" :key="social" href="#" class="text-sm font-medium text-zinc-400 hover:text-white transition-colors">
            {{ social }}
          </a>
        </div>
      </div>

      <!-- Form Pane -->
      <div class="lg:w-3/5 p-12 lg:p-16 bg-white text-zinc-900">
        <form class="space-y-8" @submit.prevent>
          <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div class="relative">
              <input type="text" id="name" class="peer w-full border-b border-zinc-300 py-2 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent" placeholder="Name">
              <label for="name" class="absolute left-0 -top-3.5 text-xs text-zinc-500 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-zinc-400 peer-placeholder-shown:top-2 peer-focus:-top-3.5 peer-focus:text-xs peer-focus:text-zinc-900">Name</label>
            </div>
            <div class="relative">
              <input type="email" id="email" class="peer w-full border-b border-zinc-300 py-2 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent" placeholder="Email">
              <label for="email" class="absolute left-0 -top-3.5 text-xs text-zinc-500 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-zinc-400 peer-placeholder-shown:top-2 peer-focus:-top-3.5 peer-focus:text-xs peer-focus:text-zinc-900">Email Address</label>
            </div>
          </div>
          
          <div class="relative">
            <input type="text" id="subject" class="peer w-full border-b border-zinc-300 py-2 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent" placeholder="Subject">
            <label for="subject" class="absolute left-0 -top-3.5 text-xs text-zinc-500 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-zinc-400 peer-placeholder-shown:top-2 peer-focus:-top-3.5 peer-focus:text-xs peer-focus:text-zinc-900">Subject</label>
          </div>
          
          <div class="relative">
            <textarea id="message" rows="4" class="peer w-full border-b border-zinc-300 py-2 placeholder-transparent focus:outline-none focus:border-zinc-900 transition-colors bg-transparent resize-none" placeholder="Project Details"></textarea>
            <label for="message" class="absolute left-0 -top-3.5 text-xs text-zinc-500 transition-all peer-placeholder-shown:text-base peer-placeholder-shown:text-zinc-400 peer-placeholder-shown:top-2 peer-focus:-top-3.5 peer-focus:text-xs peer-focus:text-zinc-900">Project Details</label>
          </div>
          
          <div class="pt-4">
            <button type="submit" class="px-8 py-4 bg-zinc-900 text-white font-medium rounded-full hover:bg-zinc-800 transition-colors w-full sm:w-auto flex items-center justify-center">
              Send Message
              <svg class="w-4 h-4 ml-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path></svg>
            </button>
          </div>
        </form>
      </div>
      
    </div>
  </section>
</template>