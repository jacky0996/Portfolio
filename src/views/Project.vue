<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const allProjects = ref([
  {
    id: 1,
    title: '個人作品集網站 (前端與 CI/CD 實作)',
    description: '使用 Vue 3 與 Tailwind CSS 打造的全響應式極簡作品集網站，並串接 GitHub Actions 與 Azure 伺服器實現自動化部署。',
    content: '本專案的最大挑戰是如何在保持極簡頁面設計的同時，從零到有建立一套完整的軟體發布流程。前端採用 Vite 與 Vue 3 建構，樣式使用 Tailwind CSS V4 進行全響應式撰寫；基礎設施則選用微軟 Azure 虛擬主機，並寫入 Dockerfile 進行容器化封裝。最後搭配 GitHub Actions 設計 Pipeline，順利達成 CI/CD 自動化。',
    image: '/portfolio/image.png',
    gallery: [
      { url: '/portfolio/image_1.png', caption: 'Azure 伺服器資源配置畫面' },
      { url: '/portfolio/image_2.png', caption: 'GitHub Actions 的 CI/CD Pipeline 自動化流程截圖' }
    ],
    tags: ['Vue 3', 'Tailwind', 'Docker', 'Azure', 'CI/CD'],
    date: '2026-03'
  },
  {
    id: 2,
    title: '資料分析儀表板',
    description: '一個供內部使用的資料視覺化儀表板，具備輕量級圖表與全響應式設計。',
    content: '這套內部工具幫助產品營運團隊能即時地追蹤各項數據指標。在此開發過程中最關鍵的挑戰在於處理數以萬筆資料載入時的「效能優化」。',
    tags: ['Javascript', 'Chart.js', 'Dashboard'],
    date: '2025-05'
  },
  {
    id: 3,
    title: '行動應用程式活動頁',
    description: '具備平滑捲動動畫與現代字體排印的高轉換率活動入口網站。',
    content: '為產品正式發布所開發的全響應式入口頁面，藉由純客製化的 CSS 動態效果，將產品特色無縫呈現在使用者眼前。',
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
        所有專案作品
      </h1>
      
      <div class="space-y-12">
        <article v-for="project in allProjects" :key="project.id" class="flex flex-col md:flex-row gap-8 items-start border p-6 rounded-2xl hover:shadow-lg transition-shadow bg-white">
          <div class="w-full md:w-1/3 h-48 sm:h-64 bg-gray-100 rounded-xl flex items-center justify-center text-gray-400 overflow-hidden relative">
            <template v-if="project.image">
              <img :src="project.image" :alt="project.title" class="w-full h-full object-cover transform group-hover:scale-105 transition-transform duration-500" />
            </template>
            <template v-else>
              [作品預覽圖]
            </template>
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
                閱讀案例詳情 →
              </router-link>
            </div>
          </div>
        </article>
      </div>
    </div>

    <!-- Detail View -->
    <div v-else-if="currentProject" class="max-w-3xl mx-auto py-8">
      <router-link to="/project" class="inline-flex items-center text-secondary hover:text-accent font-medium mb-8 transition-colors">
        ← 返回專案列表
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

      <div class="w-full md:h-[32rem] bg-gray-100 rounded-2xl mb-12 flex items-center justify-center text-gray-400 text-xl font-medium shadow-inner overflow-hidden">
        <template v-if="currentProject.image">
          <img :src="currentProject.image" :alt="currentProject.title" class="w-full h-full object-cover" />
        </template>
        <template v-else>
          [專案主視圖]
        </template>
      </div>

      <div class="prose prose-lg max-w-none text-secondary">
        <p class="text-xl leading-relaxed mb-6 font-light">
          {{ currentProject.description }}
        </p>
        <p class="leading-relaxed">
          {{ currentProject.content }}
        </p>
        
        <!-- Gallery Section 呈現更多專案照片 -->
        <template v-if="currentProject.gallery && currentProject.gallery.length > 0">
          <div class="my-12 space-y-12">
            <figure v-for="(img, idx) in currentProject.gallery" :key="idx" class="m-0">
              <div class="rounded-xl overflow-hidden border border-gray-200 shadow-sm bg-gray-50 flex justify-center p-2 md:p-4">
                <img :src="img.url" :alt="img.caption" class="max-w-full h-auto rounded-lg" />
              </div>
              <figcaption class="text-center text-sm tracking-wide text-gray-500 mt-4 font-medium">{{ img.caption }}</figcaption>
            </figure>
          </div>
        </template>

        <h3 class="text-2xl font-bold mt-12 mb-4 text-primary" v-if="!currentProject.gallery">開發挑戰與解決方案</h3>
        <p class="leading-relaxed" v-if="!currentProject.gallery">
          這裡可以詳細介紹專案在開發過程中所面臨的挑戰，以及你們是如何應用特定技術棧來克服這些問題的。
        </p>
      </div>
    </div>
    
    <!-- Not Found -->
    <div v-else class="text-center py-20">
      <h2 class="text-3xl font-bold text-primary mb-4">找不到該專案</h2>
      <router-link to="/project" class="text-accent hover:underline">返回專案列表</router-link>
    </div>
  </div>
</template>
