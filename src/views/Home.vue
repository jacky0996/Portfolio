<script setup>
import { ref } from 'vue'

const projects = ref([
  {
    id: 2,
    title: '自動化社群互動與爬蟲系統',
    description: '基於 Python 構建的全自動排程發文系統，整合 Playwright 爬蟲與 Docker 進行一鍵部署還原。',
    image: '/automation/auto_2.png',
    tags: ['Python', 'Playwright', 'MySQL', 'Docker']
  },
  {
    id: 3,
    title: 'EDM 營銷與成員管理系統',
    description: '整合企業級 SSO 驗證、大規模 Excel 處理與高效能數據維護的現代化營銷管理平台。',
    image: '/edm/edm05.png',
    tags: ['Vue 3', 'Vben Admin', 'SSO 介接', 'SA 文件撰寫', 'Excel 集成']
  },
  {
    id: 5,
    title: '歷年多元實務開發案例彙整',
    description: '因受 NDA 限制無法公開原始碼的各類企業專案，包含大型遊戲入口與 SAP/CRM 整合。',
    image: '/portfolio/image_1.png',
    tags: ['系統架構', '前後端整合', '資安維運', '實踐經驗']
  }

])
</script>

<template>
  <div class="space-y-16">
    <!-- Hero Section -->
    <section class="py-12 md:py-24 animate-fade-in-up">
      <h1 class="text-4xl md:text-6xl font-extrabold text-primary mb-6 leading-tight">
        作品集
      </h1>
      <p class="text-xl md:text-2xl text-secondary max-w-2xl font-light leading-relaxed">
        本網站使用 Vue 3 與 Tailwind CSS 建構前端畫面，並透過 Azure 主機搭配 Docker 及 GitHub Actions 實作 CI/CD 自動化部署流程。
      </p>
      <div class="mt-10">
        <router-link to="/project" class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-accent hover:bg-blue-600 transition-colors focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-accent">
          查看我的作品
        </router-link>
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
