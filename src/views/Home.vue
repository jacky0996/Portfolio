<script setup>
import { ref } from 'vue'

const projects = ref([
  {
    id: 6,
    title: 'Job Digger 職缺採集與管理生態系',
    description: '由 FastAPI 爬蟲、Laravel 後台與身分中台串成的三層架構，自動採集並清洗 104 職缺資料。',
    image: '/job_digger/start.png',
    tags: ['Python', 'FastAPI', 'Playwright', 'Laravel 11', 'SSO', 'Docker']
  },
  {
    id: 7,
    title: 'Ask Shane：RAG 履歷問答機器人',
    description: '答案只來自我真實的履歷與專案文件，逐題附上來源，查不到就誠實說不知道。',
    image: '/ask_shane/view.png',
    tags: ['Python 3', 'RAG', 'Gemini', 'Chroma', 'Cloud Run']
  },
  {
    id: 2,
    title: '自動化社群互動與爬蟲系統',
    description: '基於 Python 構建的全自動排程發文系統，整合 Playwright 爬蟲與 Docker 進行一鍵部署還原。',
    image: '/automation/auto_2.png',
    tags: ['Python', 'Playwright', 'MySQL', 'Docker']
  }

])
</script>

<template>
  <div class="space-y-16">
    <!-- Hero Section -->
    <section class="py-12 md:py-24 animate-fade-in-up">
      <div class="text-xl md:text-2xl text-secondary max-w-2xl font-light leading-relaxed space-y-2">
        <p>軟體開發經歷 6 年以上，包含管理職近 2 年</p>
        <p>擅長跨部門溝通、系統規劃</p>
        <p>仍然會追尋新技術並安排學習進度</p>
      </div>
      <div class="mt-10 flex flex-wrap gap-4">
        <router-link to="/project" class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-accent hover:bg-blue-600 transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-accent">
          查看我的作品
        </router-link>
        <a href="https://ask-shane-1036164298301.asia-east1.run.app/" target="_blank" rel="noopener noreferrer"
          class="inline-flex items-center px-6 py-3 border border-accent text-base font-medium rounded-md text-accent bg-white hover:bg-blue-50 transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-accent">
          💬 問問 Ask Shane
        </a>
        <a href="/林楨祥.pdf" target="_blank" rel="noopener noreferrer"
          class="inline-flex items-center px-6 py-3 border border-gray-300 text-base font-medium rounded-md text-primary bg-white hover:bg-gray-50 transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-300">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
          </svg>
          下載 104 履歷 (PDF)
        </a>
      </div>
    </section>

    <!-- Featured Projects Preview -->
    <section class="py-12">
      <div class="flex justify-between items-end mb-8">
        <h2 class="text-3xl font-bold text-primary">精選作品</h2>
        <router-link to="/project" class="text-accent hover:text-blue-600 font-medium transition-colors">查看全部 →</router-link>
      </div>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="project in projects" :key="project.id" class="group bg-white rounded-xl shadow-sm hover:shadow-md transition-all duration-300 overflow-hidden border border-gray-100 flex flex-col h-full transform hover:-translate-y-1">
          <div class="h-48 bg-gray-50 w-full rounded-t-xl group-hover:bg-gray-100 transition-colors flex items-center justify-center text-gray-400 overflow-hidden relative">
            <template v-if="project.image">
              <img :src="project.image" :alt="project.title" class="w-full h-full object-contain p-2 transform group-hover:scale-105 transition-transform duration-500" />
            </template>
            <template v-else>
              [作品預覽圖]
            </template>
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
              觀看案例詳情
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
