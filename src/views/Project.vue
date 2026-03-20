<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const allProjects = ref([
  {
    id: 1,
    title: 'E-commerce Redesign',
    description: 'A minimalist redesign of a modern e-commerce platform using Vue 3 and Tailwind CSS.',
    content: 'Long form content explaining the process, challenges, and solutions for the e-commerce redesign project. We focused on reducing user friction and improving checkout conversions.',
    tags: ['Vue 3', 'Tailwind', 'UI/UX'],
    date: '2025-01'
  },
  {
    id: 2,
    title: 'Dashboard Analytics',
    description: 'An internal dashboard for data visualization with lightweight charts and responsive design.',
    content: 'This internal tool helped the product team visualize metrics in real-time. Performance optimization was key here.',
    tags: ['Javascript', 'Chart.js', 'Dashboard'],
    date: '2025-05'
  },
  {
    id: 3,
    title: 'Mobile App Landing Page',
    description: 'A high-conversion landing page with smooth scroll animations and modern typography.',
    content: 'Developed a completely responsive landing page with custom CSS animations to show product features seamlessly.',
    tags: ['HTML', 'CSS', 'Framer Motion'],
    date: '2026-02'
  }
])

const isSingleProject = computed(() => {
  return route.params.id !== '' && route.params.id !== undefined
})

const currentProject = computed(() => {
  if (isSingleProject.value) {
    return allProjects.value.find(p => p.id === parseInt(route.params.id))
  }
  return null
})
</script>

<template>
  <div class="space-y-12">
    <!-- List View -->
    <div v-if="!isSingleProject">
      <h1 class="text-4xl md:text-5xl font-bold text-primary mb-8 border-b pb-4">
        All Projects
      </h1>
      
      <div class="space-y-12">
        <article v-for="project in allProjects" :key="project.id" class="flex flex-col md:flex-row gap-8 items-start border p-6 rounded-2xl hover:shadow-lg transition-shadow bg-white">
          <div class="w-full md:w-1/3 h-48 sm:h-64 bg-gray-100 rounded-xl flex items-center justify-center text-gray-400">
            [Image/Mockup]
          </div>
          <div class="w-full md:w-2/3 flex flex-col justify-center h-full space-y-4">
            <h2 class="text-3xl font-bold text-primary">
              <router-link :to="`/project/${project.id}`" class="hover:text-accent transition-colors">
                {{ project.title }}
              </router-link>
            </h2>
            <div class="flex items-center text-sm text-gray-500 space-x-4">
              <span class="font-mono">{{ project.date }}</span>
            </div>
            <p class="text-lg text-secondary leading-relaxed">{{ project.description }}</p>
            <div class="flex flex-wrap gap-2 pt-2">
              <span v-for="tag in project.tags" :key="tag" class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold tracking-wide">
                {{ tag }}
              </span>
            </div>
            <div class="pt-4">
              <router-link :to="`/project/${project.id}`" class="inline-flex items-center text-accent font-semibold hover:underline">
                Read Case Study →
              </router-link>
            </div>
          </div>
        </article>
      </div>
    </div>

    <!-- Detail View -->
    <div v-else-if="currentProject" class="max-w-3xl mx-auto py-8">
      <router-link to="/project" class="inline-flex items-center text-secondary hover:text-accent font-medium mb-8 transition-colors">
        ← Back to Projects
      </router-link>
      
      <h1 class="text-4xl md:text-5xl font-extrabold text-primary mb-6 leading-tight">
        {{ currentProject.title }}
      </h1>
      
      <div class="flex items-center space-x-6 mb-10 border-b pb-6">
        <span class="text-sm font-mono text-gray-400">{{ currentProject.date }}</span>
        <div class="flex gap-2">
          <span v-for="tag in currentProject.tags" :key="tag" class="px-2.5 py-1 bg-blue-50 text-accent text-xs rounded-md font-medium">
            {{ tag }}
          </span>
        </div>
      </div>

      <div class="w-full h-64 md:h-96 bg-gray-100 rounded-2xl mb-12 flex items-center justify-center text-gray-400 text-xl font-medium shadow-inner">
        [Main Project Image / Hero]
      </div>

      <div class="prose prose-lg max-w-none text-secondary">
        <p class="text-xl leading-relaxed mb-6 font-light">
          {{ currentProject.description }}
        </p>
        <p class="leading-relaxed">
          {{ currentProject.content }}
        </p>
        
        <h3 class="text-2xl font-bold mt-12 mb-4 text-primary">Key Challenges</h3>
        <p class="leading-relaxed">
          Detailed explanation of the challenges faced during the project and how they were overcome using the chosen tech stack.
        </p>
      </div>
    </div>
    
    <!-- Not Found -->
    <div v-else class="text-center py-20">
      <h2 class="text-3xl font-bold text-primary mb-4">Project not found</h2>
      <router-link to="/project" class="text-accent hover:underline">Return to projects</router-link>
    </div>
  </div>
</template>
