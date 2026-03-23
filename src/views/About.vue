<script setup>
import { ref } from 'vue'

const info = ref({
    name: "Shane Lin",
    role: "軟體工程師",
    location: "台北, 台灣",
    email: "z9027606@gmail.com"
})

const experiences = ref([
    {
        id: 1,
        period: "2024/07 - 至今",
        company: "華電聯網股份有限公司",
        role: "高級工程師",
        description: [
            "系統維護：負責CRM與SAP對接並進行功能開發或優化",
            "專案管理：負責CRM系統的ISSUE排程以及需求訪談",
            "資安維運：CRM系統主機內的資安問題修復或插件升級",
            "建立基礎CI/CD，整合版本控制與自動化部署，提升系統交付效率"
        ]
    },
    {
        id: 2,
        period: "2022/09 - 2024/06",
        company: "掘夢網股份有限公司",
        role: "網頁設計部主管",
        description: [
            "管理網頁設計部工作排程",
            "替部門同仁安排學習作業及方向指導",
            "舊有專案優化,維護,問題修正",
            "引入GIT作為版控,也指導同仁使用",
            "明確劃分前後端分離",
            "前端技術導入Vue"
        ]
    },
    {
        id: 3,
        period: "2021/05 - 2022/06",
        company: "和信超媒體股份有限公司",
        role: "初階後端工程師",
        description: [
            "平台功能開發，維護",
            "串接API,撰寫API",
            "舊系統翻新",
            "完成主管交代事項（優化系統）"
        ]
    },
    {
        id: 4,
        period: "2019/11 - 2021/04",
        company: "某森德網站設計公司",
        role: "後端助理工程師",
        description: [
            "網頁前後端串接",
            "後台功能開發",
            "網頁切版",
            "完成主管交辦事項",
        ]
    }
])

const professionalWorks = ref([
    {
        id: 1,
        projectId: 4,
        title: 'CRM 派工系統優化流程與自動派工',
        company: '華電聯網 (目前運作中)',
        description: '負責維護企業內部核心 CRM 系統，透過優化派工流程與導入自動化機制，有效節省人力成本並解決繁瑣重複的手動事項，顯著提升開發團隊與維運團隊的執行效率。',
        techStack: ['Laravel', 'Workflow Optimization', 'MySQL', 'Linux'],
        status: 'Live',
        note: '※ 受保密條款保護，機敏資料不可對外公開'
    },
    {
        id: 2,
        projectId: 5,
        title: '掘夢網大型遊戲官方入口與管理平台',
        company: '掘夢網 (目前運作中)',
        description: '主導多款線上遊戲官網的架構翻新與前後端分離實作。成功將專案遷移至 Vue 3 核心開發模式，並建立 Git 工作流規範與自動化部署流程，大幅提升了開發效率與跨部門協作的程式穩定度。',
        techStack: ['Vue 3', 'PHP', 'jQuery', 'Git'],
        status: 'Live',
        link: 'https://www.digeam.com/',
        note: '※ 受 NDA 協議保護，僅展示公開界面成果'
    }
])

const skills = ref(["PHP(Laravel)", "JavaScript", "jQuery", "Git", "Docker", "Vue3", "Python", "MySQL", "Linux基礎指令", "CI/CD", "Nginx"])
</script>

<template>
    <div class="py-12 md:py-20 animate-fade-in-up space-y-24">

        <!-- Section 1: Intro & Photo -->
        <section class="flex flex-col md:flex-row gap-12 items-start">
            <!-- Profile Image -->
            <div class="w-full md:w-1/3 shrink-0">
                <div class="aspect-square bg-gray-100 rounded-2xl shadow-inner overflow-hidden relative group">
                    <img src="/photo.jpg" alt="Profile"
                        class="w-full h-full object-cover transform group-hover:scale-105 transition-transform duration-500" />
                </div>
            </div>

            <!-- Brief Info & Bio -->
            <div class="w-full md:w-2/3 flex flex-col justify-center h-full pt-4 md:pt-0">
                <h1 class="text-4xl md:text-5xl font-extrabold text-primary mb-2">
                    您好，我是 {{ info.name }}
                </h1>
                <p class="text-xl text-accent font-medium mb-8">{{ info.role }}</p>

                <!-- Information List -->
                <ul class="space-y-3 mb-8 text-secondary text-sm md:text-base">
                    <li class="flex items-center">
                        <span class="w-24 font-semibold text-primary">所在地</span>
                        <span>{{ info.location }}</span>
                    </li>
                    <li class="flex items-center">
                        <span class="w-24 font-semibold text-primary">電子郵件</span>
                        <a :href="'mailto:' + info.email" class="hover:text-accent transition-colors">{{ info.email
                        }}</a>
                    </li>
                </ul>

                <div class="prose prose-lg text-secondary leading-relaxed">
                    <p>
                        累積約 6 年前後端開發經驗，從後端助理工程師一路成長為現任高級工程師，也曾擔任部門主管，負責技術決策與團隊帶領。
                    </p>
                    <p>
                        這段歷程讓我逐漸從單純的工程實作者，轉變為能兼顧技術深度與整體系統思維的工程師。
                    </p>
                </div>
            </div>
        </section>

        <!-- Section 2: Experience (經歷) -->
        <section>
            <h2 class="text-3xl font-bold text-primary mb-10 pb-4 border-b border-gray-100 flex items-center">
                <span class="bg-accent w-2 h-8 mr-4 rounded-full"></span>
                工作經歷
            </h2>

            <div class="space-y-12 pl-6 md:pl-0">
                <div v-for="exp in experiences" :key="exp.id" class="relative pl-8 md:pl-0">

                    <div class="flex flex-col md:flex-row gap-4 md:gap-12 md:items-start group">
                        <!-- Timeline Line (Mobile) -->
                        <div
                            class="absolute left-0 top-0 bottom-[-3rem] w-px bg-gray-200 md:hidden last:bg-transparent">
                        </div>
                        <!-- Timeline Dot (Mobile) -->
                        <div
                            class="absolute left-[-5px] top-2 w-3 h-3 rounded-full bg-accent md:hidden ring-4 ring-white">
                        </div>

                        <!-- Date -->
                        <div class="md:w-1/4 shrink-0 pt-1">
                            <span class="text-sm font-mono text-gray-500 group-hover:text-accent transition-colors">{{
                                exp.period }}</span>
                        </div>

                        <!-- Details -->
                        <div class="md:w-3/4 pb-8 md:pb-0 md:border-l md:border-gray-200 md:pl-10 relative">
                            <!-- Timeline Dot (Desktop) -->
                            <div
                                class="hidden md:block absolute left-[-6px] top-2 w-3 h-3 rounded-full bg-gray-300 group-hover:bg-accent transition-colors ring-4 ring-white">
                            </div>

                            <h3 class="text-xl font-bold text-primary mb-1">{{ exp.role }}</h3>
                            <p class="text-accent font-medium mb-4">{{ exp.company }}</p>
                            <ul class="list-disc leading-relaxed text-secondary pl-5 space-y-1.5 marker:text-gray-400">
                                <li v-for="(item, index) in exp.description" :key="index">
                                    {{ item }}
                                </li>
                            </ul>
                        </div>
                    </div>

                </div>
            </div>
        </section>



        <!-- Section 2.5: Professional Projects (工作專案實績) -->
        <section>
            <div
                class="flex flex-col md:flex-row md:items-end justify-between mb-10 pb-4 border-b border-gray-100 gap-4">
                <h2 class="text-3xl font-bold text-primary flex items-center">
                    <span class="bg-accent w-2 h-8 mr-4 rounded-full"></span>
                    工作專案實績 (Professional Highlights)
                </h2>
                <p class="text-xs text-secondary italic font-light">※ 包含受 NDA 保護之實務開發成果</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div v-for="work in professionalWorks" :key="work.id"
                    class="group bg-white border border-gray-100 rounded-2xl p-8 shadow-sm hover:shadow-xl transition-all duration-500 relative flex flex-col h-full border-t-4 border-t-transparent hover:border-t-accent">

                    <div class="flex justify-between items-start mb-6">
                        <div
                            class="px-3 py-1 bg-green-50 text-green-600 text-[10px] font-extrabold uppercase tracking-widest rounded-md border border-green-100">
                            {{ work.status === 'Live' ? '運作中 / Live Interface' : '內部系統' }}
                        </div>
                        <span class="text-xs font-mono text-accent font-semibold">{{ work.company }}</span>
                    </div>

                    <h3 class="text-2xl font-bold text-primary mb-4 group-hover:text-accent transition-colors">
                        <router-link v-if="work.projectId" :to="`/project/${work.projectId}`" class="hover:underline">
                            {{ work.title }}
                        </router-link>
                        <template v-else>{{ work.title }}</template>
                    </h3>

                    <p class="text-secondary text-sm leading-relaxed mb-8 flex-grow">
                        {{ work.description }}
                    </p>

                    <div class="space-y-6 mt-auto">
                        <div class="flex flex-wrap gap-2">
                            <span v-for="tech in work.techStack" :key="tech"
                                class="px-2.5 py-1 bg-gray-50 text-gray-500 text-[10px] font-extrabold rounded border border-gray-200 uppercase tracking-tighter">
                                {{ tech }}
                            </span>
                        </div>

                        <div class="pt-6 border-t border-gray-50 flex items-center justify-between">
                            <div class="flex items-center text-gray-400 text-[11px] font-medium italic">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5 mr-1.5 opacity-70"
                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
                                </svg>
                                {{ work.note }}
                            </div>
                        <div class="flex items-center gap-4">
                            <router-link v-if="work.projectId" :to="`/project/${work.projectId}`"
                                class="inline-flex items-center text-primary text-sm font-bold hover:text-accent transition-colors group/case">
                                專案詳細說明
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 ml-1 transform group-hover/case:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
                                </svg>
                            </router-link>
                            <a v-if="work.link" :href="work.link" target="_blank" rel="noopener noreferrer"
                                class="inline-flex items-center text-accent text-sm font-bold hover:underline transition-colors group/link">
                                造訪公開介面
                                <svg xmlns="http://www.w3.org/2000/svg"
                                    class="h-4 w-4 ml-1 transform group-hover/link:translate-x-1 transition-transform"
                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                        d="M14 5l7 7-7 7" />
                                </svg>
                            </a>
                        </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section 3: Skills -->
        <section>
            <h2 class="text-3xl font-bold text-primary mb-8 flex items-center">
                <span class="bg-gray-300 w-2 h-8 mr-4 rounded-full"></span>
                核心技能
            </h2>
            <div class="flex flex-wrap gap-3">
                <span v-for="skill in skills" :key="skill"
                    class="px-4 py-2 bg-white border border-gray-200 rounded-lg text-sm font-semibold text-primary shadow-sm hover:shadow-md transition-shadow">
                    {{ skill }}
                </span>
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
