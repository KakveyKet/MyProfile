<script setup>
const timelineEvents = [
  {
    date: '2025 - Present',
    title: 'Working at Trax Appareal Cambodia at Phnom Penh as Programmer (Local Young Talent)',
    description: 'Based on the project requirement, I convert the manual work to use the technology to save time and make the system or RPA auto work. I also study about the bussiness process and flow about the factory to make the system (Export Management System, Inventory Management System, and etc) that can help the company to save time and make the work more efficient.'
  },
  {
    date: '2024 - 2025',
    title: 'Working as Front end Developer at Battambang (Master IT Co., Ltd.)',
    description: 'Based on the project requirement, I developed the front end of the web app using Vue,js, React Js, and Tailwind CSS. I also collaborated with the backend team to integrate APIs and ensure seamless functionality. And also usig WordPress to build the websute for company and client too.'
  },
  {
    date: '2022 — 2023',
    title: 'Intern as IT Support & Web Developer',
    description: 'Developed internal scanning attendance & controlling the computer lab and report about the inventory of the computer lab. Training the staff and students to use the system. And also developed the website for the University to use the E-Learning platform andE-library.'
  },
  {
    date: '2022',
    title: 'Web App Developer Intern',
    description: 'Integrated Glide App with Webhook to build a web app for managing inventory and sales data, streamlining operations for a local business.'
  },
  {
    date: '2021',
    title: 'Teaching and Lead the classmate.',
    description: 'Teaching about web dev programming such as HTML, CSS, JavaScript, Tailwind CSS, and React js  to the classmate and also lead the classmate to do the project together.'
  }

]
</script>

<template>
  <section id="timeline" class="scroll-mt-32">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-start">

      <div class="lg:col-span-4">
        <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Experience</h2>
        <h3 class="text-3xl font-bold text-zinc-900">Career Journey.</h3>
      </div>

      <div class="lg:col-span-8">
        <div class="relative border-l border-zinc-200 pl-8 space-y-12 ml-2">
          <div v-for="(event, index) in timelineEvents" :key="index" class="relative group">
            <!-- Sleek indicator dot -->
            <div
              class="absolute -left-[37px] top-1.5 h-2.5 w-2.5 rounded-full bg-zinc-300 group-hover:bg-zinc-900 transition-colors ring-4 ring-zinc-50">
            </div>

            <span class="text-xs font-semibold text-zinc-400 tracking-widest uppercase mb-1 block">{{ event.date
              }}</span>
            <h4 class="text-xl font-bold text-zinc-900 mb-2">{{ event.title }}</h4>
            <p class="text-zinc-600 font-light leading-relaxed max-w-2xl">{{ event.description }}</p>
          </div>
        </div>
      </div>

    </div>
  </section>
</template>