<script setup>
import { ref } from 'vue'

const projects = ref([
  {
    id: 1,
    title: 'E-commerce Redesign',
    description: 'A minimalist redesign of a modern e-commerce platform using Vue 3 and Tailwind CSS.',
    tags: ['Vue 3', 'Tailwind', 'UI/UX']
  },
  {
    id: 2,
    title: 'Dashboard Analytics',
    description: 'An internal dashboard for data visualization with lightweight charts and responsive design.',
    tags: ['Javascript', 'Chart.js', 'Dashboard']
  },
  {
    id: 3,
    title: 'Mobile App Landing Page',
    description: 'A high-conversion landing page with smooth scroll animations and modern typography.',
    tags: ['HTML', 'CSS', 'Framer Motion']
  }
])
</script>

<template>
  <div class="space-y-16">
    <!-- Hero Section -->
    <section class="py-12 md:py-24 animate-fade-in-up">
      <h1 class="text-4xl md:text-6xl font-extrabold text-primary mb-6 leading-tight">
        Hello. I'm a Creator.
      </h1>
      <p class="text-xl md:text-2xl text-secondary max-w-2xl font-light leading-relaxed">
        I build beautiful, minimalist web experiences that focus on what matters most.
      </p>
      <div class="mt-10">
        <router-link to="/project" class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-accent hover:bg-blue-600 transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-accent">
          View My Work
        </router-link>
      </div>
    </section>

    <!-- Featured Projects Preview -->
    <section class="py-12">
      <div class="flex justify-between items-end mb-8">
        <h2 class="text-3xl font-bold text-primary">Featured Work</h2>
        <router-link to="/project" class="text-accent hover:text-blue-600 font-medium transition-colors">See all →</router-link>
      </div>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="project in projects" :key="project.id" class="group bg-white rounded-xl shadow-sm hover:shadow-md transition-all duration-300 overflow-hidden border border-gray-100 flex flex-col h-full transform hover:-translate-y-1">
          <div class="h-48 bg-gray-100 w-full rounded-t-xl group-hover:bg-gray-200 transition-colors flex items-center justify-center text-gray-400">
            [Project Image]
          </div>
          <div class="p-6 flex flex-col flex-grow">
            <h3 class="text-xl font-bold text-primary mb-2 group-hover:text-accent transition-colors">{{ project.title }}</h3>
            <p class="text-secondary text-sm mb-4 flex-grow">{{ project.description }}</p>
            <div class="flex flex-wrap gap-2 mt-auto">
              <span v-for="tag in project.tags" :key="tag" class="px-2.5 py-1 bg-blue-50 text-accent text-xs rounded-md font-medium">
                {{ tag }}
              </span>
            </div>
            <router-link :to="`/project/${project.id}`" class="mt-6 text-sm font-semibold text-primary group-hover:text-accent transition-colors flex items-center">
              View Case Study
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1 transform group-hover:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </router-link>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}

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
</style>
