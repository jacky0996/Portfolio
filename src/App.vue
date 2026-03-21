<script setup>
</script>

<template>
  <div class="min-h-screen flex flex-col font-sans">
    <header class="w-full py-6 px-4 md:px-8 flex justify-between items-center max-w-6xl mx-auto">
      <h1 class="text-xl font-bold tracking-tight text-primary">
        <router-link to="/">Shane的作品集</router-link>
      </h1>
      <nav class="space-x-6">
        <router-link to="/" class="text-secondary hover:text-accent transition-colors font-medium">首頁</router-link>
        <router-link to="/about" class="text-secondary hover:text-accent transition-colors font-medium">關於我</router-link>
        <router-link to="/project" class="text-secondary hover:text-accent transition-colors font-medium">專案作品</router-link>
      </nav>
    </header>

    <main class="flex-grow w-full max-w-6xl mx-auto px-4 md:px-8 py-8">
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>

    <footer class="w-full py-6 text-center text-sm text-gray-500 mt-auto">
      &copy; {{ new Date().getFullYear() }} Shane的作品集. All rights reserved.
    </footer>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
