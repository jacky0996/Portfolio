<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const selectedImage = ref(null)

const openModal = (url) => {
    selectedImage.value = url
}

const closeModal = () => {
    selectedImage.value = null
}

const allProjects = ref([
    {
        id: 1,
        title: '個人作品集網站',
        description: '涵蓋前端介面開發與基本的伺服器部署設定。',
        content: '實作部分主要採用 Vue 3 與 Tailwind CSS 進行版面開發。部署方面選擇 Azure 虛擬主機，並寫入 Dockerfile 進行容器化打包。最後透過 GitHub Actions 建立可自動連線更新的 CI/CD 部署流程。',
        image: '/portfolio/image.png',
        gallery: [
            { url: '/portfolio/image_1.png', caption: 'Azure 伺服器資源畫面' },
            { url: '/portfolio/image_2.png', caption: 'GitHub Actions CI/CD 流程截圖' }
        ],
        links: [
            { name: '透過專屬網域名稱造訪', url: 'http://shaneportolio.japanwest.cloudapp.azure.com', note: '若連線有問題，可能是 DNS 尚未生效配置' },
            { name: '透過主機 IP 直接造訪', url: 'http://20.18.160.75' }
        ],
        tags: ['Vue 3', 'Tailwind', 'Docker', 'Azure', 'CI/CD'],
    },
    {
        id: 2,
        title: 'PTT & CMoney 自動化社群與爬蟲系統',
        description: '基於 Python 與 Playwright 所開發的全自動化社群互動與股價爬蟲系統。',
        content: '本專案能自動存取並登入 PTT 與 CMoney 兩大論壇平台，並根據 MySQL 資料庫內設定的排程規則自動執行推文及發文。為解決動態網頁內容載入的痛點，特別整合了無頭瀏覽器 Playwright 強制模擬人類操作，準確抓取熱門股票的即時資料。系統環境全數透過 Docker Compose 進行容器化封裝，並特別撰寫了初始化啟動腳本，確保在 Docker Build 部署完成後，系統會自動預載建立好「測試帳號」與「每日測試發文功能」，實現真正開箱即用、隨開即測的自動化體驗。',
        image: '/automation/auto_2.png',
        gallery: [
            { url: '/automation/auto_4.png', caption: '自動登入結果呈現，實踐 PTT 平台與社群論壇自動登入' },
            { url: '/automation/auto_1.png', caption: '系統自動發文與事務執行紀錄的推播結果' },
            { url: '/automation/auto_3.png', caption: 'CI 行為：使用 Flake8 工具檢查語法問題及驗證 Docker Build 是否正確' }
        ],
        links: [
            { name: '前往 GitHub 專案原始碼', url: 'https://github.com/jacky0996/automation-plan' }
        ],
        tags: ['Python', 'Playwright', 'PyPtt', 'MySQL', 'Docker'],
    },
    {
        id: 3,
        title: 'EDM 營銷與成員管理系統',
        description: '整合企業級 SSO 驗證、大規模 Excel 處理與高效能數據維護的現代化營銷管理平台。',
        content: '本專案為一套專為行銷團隊打造的 EDM 管理系統。開發亮點在於我特別嘗試了「系統分析 (SA) 文件」的撰寫，包含針對 PM 與利害關係人的周報日誌與 Use Case 流程圖，確保需求轉化為功能的嚴謹度。技術上則實裝了與公司 HWS 系統的 SSO (Single Sign-On) 介接，採用一次性短期 Token 交換長期證明的機制。此方案不使用 Cookie，能有效防禦 CSRF 攻擊並支持跨網域部署，前端更實作了參數攔截與環境清理邏輯，大幅提升應用程式的安全性與使用者體驗。',
        image: '/edm/edm05.png',
        gallery: [
            { url: '/edm/edm01.png', caption: '系統開發日誌：詳細紀錄每週技術決策，利於 PM 追縱進度' },
            { url: '/edm/edm02.png', caption: 'Use Case 流程圖：在編碼前進行完整的系統邏輯規劃' },
            { url: '/edm/edm07.png', caption: '表單組件開發：封裝 API 介接邏輯，支持非同步數據驗證與提交' },
            { url: '/edm/edm08.png', caption: '高效能成員清單頁：整合 VXE Table 處理大量數據的展示與搜尋' }
        ],
        tags: ['Vue 3', 'Vben Admin', 'SSO 介接', 'SA 文件撰寫', 'Excel 集成']
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
                <article v-for="project in allProjects" :key="project.id"
                    class="flex flex-col md:flex-row gap-8 items-start border p-6 rounded-2xl hover:shadow-lg transition-shadow bg-white">
                    <div
                        class="w-full md:w-1/3 h-48 sm:h-64 bg-gray-50 rounded-xl flex items-center justify-center text-gray-400 overflow-hidden relative">
                        <template v-if="project.image">
                            <img :src="project.image" :alt="project.title"
                                class="w-full h-full object-contain p-2 transform group-hover:scale-105 transition-transform duration-500" />
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
                            <span v-for="tag in project.tags" :key="tag"
                                class="px-3 py-1 bg-gray-100 text-gray-600 rounded-full text-xs font-semibold tracking-wide">
                                {{ tag }}
                            </span>
                        </div>
                        <div class="pt-4">
                            <router-link :to="`/project/${project.id}`"
                                class="inline-flex items-center text-accent font-semibold hover:underline">
                                閱讀案例詳情 →
                            </router-link>
                        </div>
                    </div>
                </article>
            </div>
        </div>

        <!-- Detail View -->
        <div v-else-if="currentProject" class="max-w-3xl mx-auto py-8">
            <router-link to="/project"
                class="inline-flex items-center text-secondary hover:text-accent font-medium mb-8 transition-colors">
                ← 返回專案列表
            </router-link>

            <h1 class="text-4xl md:text-5xl font-extrabold text-primary mb-6 leading-tight">
                {{ currentProject.title }}
            </h1>

            <div class="flex items-center space-x-6 mb-10 border-b pb-6">
                <span class="text-sm font-mono text-gray-400">{{ currentProject.date }}</span>
                <div class="flex gap-2">
                    <span v-for="tag in currentProject.tags" :key="tag"
                        class="px-2.5 py-1 bg-blue-50 text-accent text-xs rounded-md font-medium">
                        {{ tag }}
                    </span>
                </div>
            </div>

            <div
                class="w-full md:h-[32rem] bg-gray-50 rounded-2xl mb-12 flex items-center justify-center text-gray-400 text-xl font-medium shadow-inner overflow-hidden">
                <template v-if="currentProject.image">
                    <img :src="currentProject.image" :alt="currentProject.title"
                        class="w-full h-full object-contain p-4 cursor-zoom-in hover:opacity-90 transition-opacity"
                        @click="openModal(currentProject.image)" />
                </template>
                <template v-else>
                    [專案主視圖]
                </template>
            </div>

            <div class="prose prose-lg max-w-none text-secondary">
                <p class="text-xl leading-relaxed mb-6 font-light">
                    {{ currentProject.description }}
                </p>

                <!-- 外部連結按鈕 -->
                <template v-if="currentProject.links && currentProject.links.length > 0">
                    <div class="flex flex-wrap gap-6 mb-8 mt-4 not-prose">
                        <div v-for="link in currentProject.links" :key="link.url" class="flex flex-col">
                            <a :href="link.url" target="_blank" rel="noopener noreferrer"
                                class="inline-flex items-center justify-center px-5 py-2.5 border border-transparent text-sm font-medium rounded-full shadow-md text-white bg-primary hover:bg-accent transition-colors shrink-0 whitespace-nowrap">
                                {{ link.name }}
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-2" fill="none"
                                    viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
                                </svg>
                            </a>
                            <span v-if="link.note" class="text-xs text-gray-500 mt-2 ml-1 opacity-80">*{{ link.note
                                }}</span>
                        </div>
                    </div>
                </template>

                <p class="leading-relaxed">
                    {{ currentProject.content }}
                </p>

                <!-- Gallery Section 呈現更多專案照片 -->
                <template v-if="currentProject.gallery && currentProject.gallery.length > 0">
                    <div class="my-12 space-y-12">
                        <figure v-for="(img, idx) in currentProject.gallery" :key="idx" class="m-0">
                            <div
                                class="rounded-xl overflow-hidden border border-gray-200 shadow-sm bg-gray-50 flex justify-center p-2 md:p-4">
                                <img :src="img.url" :alt="img.caption"
                                    class="max-w-full h-auto rounded-lg object-contain cursor-zoom-in hover:opacity-90 transition-opacity"
                                    @click="openModal(img.url)" />
                            </div>
                            <figcaption class="text-center text-sm tracking-wide text-gray-500 mt-4 font-medium">{{
                                img.caption }}</figcaption>
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

        <!-- Image Modal -->
        <transition name="fade">
            <div v-if="selectedImage"
                class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-sm p-4 cursor-zoom-out"
                @click="closeModal">
                <button
                    class="absolute top-6 right-6 text-white hover:text-gray-300 transform hover:scale-110 transition-all font-bold text-3xl z-50">
                    ✕
                </button>
                <img :src="selectedImage"
                    class="max-h-[85vh] max-w-[90vw] object-contain rounded-lg shadow-2xl cursor-default" @click.stop />
            </div>
        </transition>
    </div>
</template>
