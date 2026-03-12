<script setup>
const skillCategories = [
  {
    title: 'Frontend Development',
    skills: ['Vue.js', 'React', 'JavaScript (ES6+)', 'Tailwind CSS', 'HTML5/CSS3']
  },
  {
    title: 'Backend & Databases',
    skills: ['Node.js', 'Python', 'Django', 'REST APIs', 'MySQL', 'MongoDB']
  },
  {
    title: 'Tools & Architecture',
    skills: ['Git & GitHub', 'Figma', 'System Automation', 'Agile/Scrum']
  }
]
</script>

<template>
  <section id="skills" class="scroll-mt-32">
    <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 lg:gap-8 items-start">
      
      <div class="lg:col-span-4">
        <h2 class="text-xs font-bold text-zinc-400 uppercase tracking-widest mb-3">Expertise</h2>
        <h3 class="text-3xl font-bold text-zinc-900">Technical Arsenal.</h3>
      </div>

      <div class="lg:col-span-8 grid grid-cols-1 md:grid-cols-2 gap-10">
        <div v-for="category in skillCategories" :key="category.title">
          <h4 class="text-sm font-semibold text-zinc-900 border-b border-zinc-200 pb-2 mb-4">{{ category.title }}</h4>
          <ul class="flex flex-wrap gap-2">
            <li 
              v-for="skill in category.skills" 
              :key="skill"
              class="px-3 py-1.5 bg-white border border-zinc-200 rounded-md text-sm font-medium text-zinc-600 hover:text-zinc-900 hover:border-zinc-300 transition-colors cursor-default"
            >
              {{ skill }}
            </li>
          </ul>
        </div>
      </div>

    </div>
  </section>
</template>