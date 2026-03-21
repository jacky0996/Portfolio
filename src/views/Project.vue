<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

const allProjects = ref([
  {
    id: 1,
    title: '電商平台視覺重塑',
    description: '使用 Vue 3 與 Tailwind CSS 替現代電商平台進行的極簡風格設計重構。',
    content: '這裡可以填寫長篇幅的敘述，例如：專案的挑戰、我們如何解決購物車結帳流程的阻礙，以及我們透過重新設計幫助業主提升了多少轉換率。',
    tags: ['Vue 3', 'Tailwind', 'UI/UX'],
    date: '2025-01'
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
          <div class="w-full md:w-1/3 h-48 sm:h-64 bg-gray-100 rounded-xl flex items-center justify-center text-gray-400">
            [作品預覽圖]
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

      <div class="w-full h-64 md:h-96 bg-gray-100 rounded-2xl mb-12 flex items-center justify-center text-gray-400 text-xl font-medium shadow-inner">
        [專案主視圖]
      </div>

      <div class="prose prose-lg max-w-none text-secondary">
        <p class="text-xl leading-relaxed mb-6 font-light">
          {{ currentProject.description }}
        </p>
        <p class="leading-relaxed">
          {{ currentProject.content }}
        </p>
        
        <h3 class="text-2xl font-bold mt-12 mb-4 text-primary">開發挑戰與解決方案</h3>
        <p class="leading-relaxed">
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
