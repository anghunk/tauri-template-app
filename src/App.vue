<template>
  <div class="container">
    <h1>欢迎使用 Tauri!</h1>
    <div class="row">
      <a href="https://vitejs.dev" target="_blank">
        <img src="/vite.svg" class="logo vite" alt="Vite logo" />
      </a>
      <a href="https://vuejs.org/" target="_blank">
        <img src="/vue.svg" class="logo vue" alt="Vue logo" />
      </a>
      <a href="https://tauri.app" target="_blank">
        <img src="/tauri.svg" class="logo tauri" alt="Tauri logo" />
      </a>
    </div>

    <p>点击 Tauri、Vite 和 Vue 的 logo 了解更多信息</p>

    <form class="row mt-2 mb-2" @submit.prevent="greet">
      <input
        v-model="greetMsg"
        placeholder="输入名字..."
        class="h-9 px-3 text-sm bg-white border border-gray-200 rounded-md text-gray-900 placeholder-gray-400 outline-none transition-colors hover:border-gray-300 focus:border-gray-400 dark:bg-gray-900 dark:border-gray-700 dark:text-gray-100 dark:placeholder-gray-500 dark:hover:border-gray-600 dark:focus:border-gray-500"
      />
      <button
        type="submit"
        class="flex items-center justify-center h-9 px-3 text-sm font-medium bg-gray-900 text-white rounded-md transition-colors hover:bg-gray-800 active:bg-gray-950 dark:bg-white dark:text-gray-900 dark:hover:bg-gray-100 dark:active:bg-gray-200"
      >
        <PhRocket :size="20" class="mr-2" />
        问候
      </button>
    </form>

    <p v-if="greetResponse">{{ greetResponse }}</p>

    <div class="icon-showcase">
      <h3>Phosphor Icons 示例</h3>
      <div class="icons">
        <PhHeart :size="32" weight="fill" color="#e74c3c" />
        <PhStar :size="32" weight="fill" color="#f39c12" />
        <PhRocket :size="32" weight="duotone" color="#3498db" />
        <PhGithubLogo :size="32" weight="bold" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/core";

const greetMsg = ref("");
const greetResponse = ref("");

async function greet() {
  greetResponse.value = await invoke("greet", { name: greetMsg.value });
}
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.logo.tauri:hover {
  filter: drop-shadow(0 0 2em #24c8dbaa);
}

.icon-showcase {
  padding: 1.5rem;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.1);
}

.icon-showcase h3 {
  margin-bottom: 1rem;
  font-size: 1.2rem;
}

.icons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  align-items: center;
}
</style>
