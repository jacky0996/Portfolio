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
        content: `本專案為一套專為行銷團隊打造的 EDM 管理系統。開發亮點在於我特別嘗試了「系統分析 (SA) 文件」的撰寫，包含針對 PM 與利害關係人的周報日誌與 Use Case 流程圖，確保需求轉化為功能的嚴謹度。

在資安與權限管理層面，我們實作了與公司 HWS 系統的 SSO (Single Sign-On) 介接，採用「一次性短期 Token 交換長期證明的機制」。此架構具備三大優勢：
- **防禦 CSRF 攻擊**：捨棄 Cookie 方案，瀏覽器不會自動發送憑證，從根本上避免了跨站請求偽造。
- **解決跨網域限制**：支持 EDM (Vue) 與 HWS (Laravel) 在完全不同的網域甚至是網絡環境下對接。
- **靈活性**：權限完全由 Authorization Header 控制，適合 SPA 與 API 分離的現代架構。

實作流程如下：
1. **引導跳轉**：使用者從內部系統跳轉時，網址帶入 ?token=SSO_TOKEN。
2. **攔截與驗證**：前端路由守衛 (guard.ts) 優先檢查 URL 參數，偵測到 Token 後立即呼叫 AuthStore 進行驗證。
3. **後端換票**：前端將短期 Token 送往驗證介面，HWS 驗證通過後會註銷該短效 Token 並回傳正式 accessToken。
4. **清理與持久化**：驗證成功後使用 replace: true 移除網址參數以確保網址乾淨，並將正式 Token 儲存在 localStorage 供後續 API 請求使用。`,
        image: '/edm/edm05.png',
        gallery: [
            { url: '/edm/edm01.png', caption: '系統開發日誌：詳細紀錄每週技術決策，利於 PM 追縱進度' },
            { url: '/edm/edm02.png', caption: 'Use Case 流程圖：在編碼前進行完整的系統邏輯規劃' },
            { url: '/edm/edm07.png', caption: '表單組件開發：封裝 API 介接邏輯，支持非同步數據驗證與提交' },
            { url: '/edm/edm08.png', caption: '高效能成員清單頁：整合 VXE Table 處理大量數據的展示與搜尋' }
        ],
        links: [
            { name: '前往 GitHub 專案原始碼', url: 'https://github.com/jacky0996/EDM.git', note: '僅提供程式碼 相關介接系統暫時無法提供' }
        ],
        tags: ['Vue 3', 'Vben Admin', 'SSO 介接', 'SA 文件撰寫', 'Excel 集成']
    },
    {
        id: 4,
        title: 'CRM派工系統優化流程及自動派工',
        description: '優化現有派工系統 節省人力及繁瑣重複事項',
        content: `此專案為我於「華電聯網」期間主導開發的 CRM 核心系統優化項目，核心成果為「自動派工設定功能」。

原本公司的定期保固（定保）案件皆由客服單位統一接收後，再手動派遣給各相關單位的小組長。這種模式不僅增加了客服人員的大量行政負荷 (Loading)，也容易在人工傳達過程中產生派遣錯誤或延遲。

為了優化此流程，我開發了一套自動化的派工設定機制：
1. **跨系統整合**：串接公司內其他系統，自動獲取被指派單位的部門主管資訊。
2. **層級式管理**：由部門主管設定所屬小組長，再由小組長指派具體工程師。
3. **自動繼承與派遣**：系統會記憶此核心設定，未來該單位的定保案件將自動套用此規則進行派工，實現真正的一鍵自動化。
4. **自動化監控機制**：撰寫背景排程 (Schedule) 每週自動檢查尚未完成派工的項目，並即時寄送通知信提醒相關主管，確保案件不被遺漏。

此優化顯著降低了客服單位的維運壓力，並透過「部門主管各自領案」的模式大幅提升了派工的準確性與響應速度。`,
        image: null,
        gallery: [
            { url: '/crm/crm_01.png', caption: '定期保固清單頁面：顯示各案件及其已設定之派工單位' },
            { url: '/crm/crm_02.png', caption: '案件定保詳細頁：呈現維修案件之詳細履歷與保固內容' },
            { url: '/crm/crm_03.png', caption: '自動派工詳細資料：系統根據設定自動產生的相關處理歷程' }
        ],
        isConfidential: true,
        tags: ['CRM', '自動派工', 'Laravel', 'Workflow Optimization', '排程管理']
    },
    {
        id: 5,
        title: '歷年實務開發案例彙整',
        content: `此項目彙整了我在「掘夢網 (Digeam)」時期擔任小組主管及後端開發的重點實務貢獻。

在技術實踐層面，我主導了多個遊戲官網的「Game Mall (遊戲商城)」系統開發：
- **核心後端與數據整合**：負責金流支付 API 串接，並確保外部網域與內部遊戲實時數據的高效對接。
- **動態帳務處理**：系統能讓玩家輸入角色 ID 後，即時呼叫內部 API 獲取詳盡的角色資料與帳戶狀態，並直接進行點數與道具的購買及入點作業。

在團隊管理與流程優化層面：
- **推行前後端職責分離**：主導該公司「網頁設計部門」內部前後端開發流程的分離設定。這套科學的工作流管理模式大幅提昇了專案開發效率。
- **招聘與引才標準**：這套開發模式目前仍是該公司在招聘與篩選技術同仁時的重要評估依據。

這些實戰案例體現了我將複雜業務需求抽象化並落實為高品質代碼的能力。`,
        image: null,
        gallery: [
            { url: '/digeam/digeam_01.png', caption: '掘夢網遊戲商城 (Game Mall) - 後端數據與金流串接核心作品' },
            { url: '/digeam/digeam_03.png', caption: '角色登入介面 - 玩家輸入 ID 後系統即時連動遊戲 API' },
            { url: '/digeam/digeam_04.png', caption: '登入後介面 - 獲取角色資料並直接進行購點與商城購買行為' },
            { url: '/digeam/digeam_02.png', caption: '技術流程管理 - 實施前後端分工的最佳實踐，目前仍為公司招募標準' }
        ],
        links: [
            { name: '造訪遊戲商城專案界面', url: 'https://cbm.digeam.com/gameMall' }
        ],
        isConfidential: true,
        tags: ['後端開發', '電商金流', '流程管理', 'API 整合', 'PHP/Laravel']
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
                        <div v-if="project.isConfidential"
                            class="px-2 py-0.5 bg-amber-50 text-amber-600 rounded text-[10px] font-bold uppercase tracking-wider border border-amber-100 w-fit">
                            Commercial Case Study
                        </div>
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

            <div v-if="currentProject.isConfidential" class="mb-4">
                <span
                    class="px-2.5 py-1 bg-amber-50 text-amber-600 text-xs rounded-md font-bold border border-amber-100 uppercase tracking-tighter">
                    受保密協議 (NDA) 保護：實務案例
                </span>
            </div>

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

                <!-- 保密合約提示 -->
                <template v-else-if="currentProject.isConfidential">
                    <div class="flex flex-wrap gap-6 mb-10 mt-6 not-prose">
                        <div
                            class="inline-flex items-center justify-center px-6 py-3 border border-dashed border-amber-200 text-sm font-semibold rounded-2xl text-amber-700 bg-amber-50/30 italic">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-3 text-amber-500" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                            </svg>
                            此專案受商業保密協議限制，恕不公開原始碼及機密細節。
                        </div>
                    </div>
                </template>

                <p class="leading-relaxed whitespace-pre-line">
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
