<template>
  <div class="min-h-screen bg-white dark:bg-gray-950 text-gray-900 dark:text-gray-100">
    <!-- 导航栏 -->
    <nav
      class="fixed top-0 left-0 right-0 z-50 bg-white/80 dark:bg-gray-950/80 backdrop-blur-sm border-b border-gray-200 dark:border-gray-800"
    >
      <div class="max-w-5xl mx-auto px-6 h-14 flex items-center justify-between">
        <div class="flex items-center gap-2">
          <PhLightning :size="20" weight="fill" class="text-gray-900 dark:text-white" />
          <span class="font-medium text-sm">Tauri Template App</span>
        </div>
        <div class="flex items-center gap-6">
          <a
            href="#features"
            class="text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors"
            >特性</a
          >
          <a
            href="#demo"
            class="text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors"
            >演示</a
          >
          <button
            @click="toggleTheme"
            class="p-1.5 rounded text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 transition-colors"
          >
            <PhSun :size="18" v-if="isDark" />
            <PhMoon :size="18" v-else />
          </button>
        </div>
      </div>
    </nav>

    <!-- Hero 区域 -->
    <section class="pt-32 pb-16 px-6">
      <div class="max-w-3xl mx-auto text-center">
        <h1 class="text-4xl md:text-5xl font-semibold tracking-tight mb-4">
          下一代桌面应用开发体验
        </h1>
        <p class="text-lg text-gray-600 dark:text-gray-400 mb-8 leading-relaxed">
          使用 Web 技术构建轻量、快速、安全的桌面应用程序。 结合 Rust 的性能与 Vue
          的灵活性。
        </p>
        <div class="flex items-center justify-center gap-3">
          <button
            @click="scrollToDemo"
            class="px-5 py-2.5 bg-gray-900 dark:bg-white text-white dark:text-gray-900 rounded-lg text-sm font-medium hover:bg-gray-800 dark:hover:bg-gray-100 transition-colors"
          >
            立即体验
          </button>
          <a
            href="https://github.com/anghunk/tauri-template-app"
            target="_blank"
            class="px-5 py-2.5 bg-gray-100 dark:bg-gray-800 text-gray-700 dark:text-gray-300 rounded-lg text-sm font-medium hover:bg-gray-200 dark:hover:bg-gray-700 transition-colors"
          >
            查看源码
          </a>
        </div>
      </div>
    </section>

    <!-- Logo 展示 -->
    <section class="pb-16 px-6">
      <div class="max-w-3xl mx-auto">
        <div class="flex items-center justify-center gap-12 opacity-40">
          <a
            href="https://vitejs.dev"
            target="_blank"
            class="hover:opacity-70 transition-opacity"
          >
            <img src="/vite.svg" class="h-8" alt="Vite" />
          </a>
          <a
            href="https://vuejs.org/"
            target="_blank"
            class="hover:opacity-70 transition-opacity"
          >
            <img src="/vue.svg" class="h-8" alt="Vue" />
          </a>
          <a
            href="https://tauri.app"
            target="_blank"
            class="hover:opacity-70 transition-opacity"
          >
            <img src="/tauri.svg" class="h-8" alt="Tauri" />
          </a>
        </div>
      </div>
    </section>

    <!-- 特性展示 -->
    <section
      id="features"
      class="py-16 px-6 border-t border-gray-200 dark:border-gray-800"
    >
      <div class="max-w-5xl mx-auto">
        <div
          class="grid md:grid-cols-2 gap-px bg-gray-200 dark:bg-gray-800 rounded-lg overflow-hidden"
        >
          <div
            v-for="(feature, index) in features"
            :key="index"
            class="p-8 bg-white dark:bg-gray-950 hover:bg-gray-50 dark:hover:bg-gray-900 transition-colors"
          >
            <component
              :is="feature.icon"
              :size="24"
              class="text-gray-900 dark:text-white mb-4"
            />
            <h3 class="text-base font-medium mb-2">{{ feature.title }}</h3>
            <p class="text-sm text-gray-600 dark:text-gray-400 leading-relaxed">
              {{ feature.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- 技术栈 -->
    <section id="tech" class="py-16 px-6 border-t border-gray-200 dark:border-gray-800">
      <div class="max-w-5xl mx-auto">
        <h2 class="text-lg font-medium mb-6">技术栈</h2>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
          <div
            v-for="(tech, index) in techStack"
            :key="index"
            class="p-4 border border-gray-200 dark:border-gray-800 rounded-lg hover:border-gray-300 dark:hover:border-gray-700 transition-colors"
          >
            <component :is="tech.icon" :size="20" class="mb-3" />
            <h4 class="text-sm font-medium mb-1">{{ tech.name }}</h4>
            <p class="text-xs text-gray-600 dark:text-gray-400">{{ tech.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 交互演示 -->
    <section id="demo" class="py-16 px-6 border-t border-gray-200 dark:border-gray-800">
      <div class="max-w-2xl mx-auto">
        <h2 class="text-lg font-medium mb-6">试试看</h2>

        <div class="p-6 border border-gray-200 dark:border-gray-800 rounded-lg">
          <div class="flex flex-col md:flex-row items-center gap-3 mb-6">
            <input
              v-model="greetMsg"
              placeholder="输入你的名字..."
              class="flex-1 w-full h-10 px-4 text-sm bg-transparent border border-gray-200 dark:border-gray-800 rounded-lg text-gray-900 dark:text-white placeholder-gray-500 outline-none focus:border-gray-400 dark:focus:border-gray-600 transition-colors"
              @keyup.enter="greet"
            />
            <button
              @click="greet"
              :disabled="!greetMsg.trim() || isLoading"
              class="w-full md:w-auto px-5 h-10 bg-gray-900 dark:bg-white text-white dark:text-gray-900 rounded-lg text-sm font-medium hover:bg-gray-800 dark:hover:bg-gray-100 transition-colors disabled:opacity-50 disabled:cursor-not-allowed"
            >
              <PhSpinner :size="16" class="animate-spin inline mr-2" v-if="isLoading" />
              {{ isLoading ? "处理中..." : "发送问候" }}
            </button>
          </div>

          <Transition
            enter-active-class="transition-all duration-200"
            enter-from-class="opacity-0"
            enter-to-class="opacity-100"
          >
            <div v-if="greetResponse" class="p-4 bg-gray-50 dark:bg-gray-900 rounded-lg">
              <p class="text-xs text-gray-500 dark:text-gray-500 mb-1">Rust 后端响应</p>
              <p class="text-sm">{{ greetResponse }}</p>
            </div>
          </Transition>
        </div>

        <!-- 统计数据 -->
        <div class="grid grid-cols-3 gap-4 mt-6">
          <div
            class="p-4 border border-gray-200 dark:border-gray-800 rounded-lg text-center"
          >
            <div class="text-xl font-medium mb-1">{{ stats.appSize }}</div>
            <div class="text-xs text-gray-600 dark:text-gray-400">安装包</div>
          </div>
          <div
            class="p-4 border border-gray-200 dark:border-gray-800 rounded-lg text-center"
          >
            <div class="text-xl font-medium mb-1">{{ stats.memory }}</div>
            <div class="text-xs text-gray-600 dark:text-gray-400">内存占用</div>
          </div>
          <div
            class="p-4 border border-gray-200 dark:border-gray-800 rounded-lg text-center"
          >
            <div class="text-xl font-medium mb-1">{{ stats.startup }}</div>
            <div class="text-xs text-gray-600 dark:text-gray-400">启动时间</div>
          </div>
        </div>
      </div>
    </section>

    <!-- 页脚 -->
    <footer class="py-8 px-6 border-t border-gray-200 dark:border-gray-800">
      <div
        class="max-w-5xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4"
      >
        <span class="text-xs text-gray-500 dark:text-gray-500"
          >使用 Tauri + Vue 构建</span
        >
        <div class="flex items-center gap-4">
          <a
            href="#"
            class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-300 transition-colors"
          >
            <PhGithubLogo :size="18" />
          </a>
          <a
            href="#"
            class="text-gray-400 hover:text-gray-600 dark:hover:text-gray-300 transition-colors"
          >
            <PhTwitterLogo :size="18" />
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { invoke } from "@tauri-apps/api/core";
import {
  PhLightning,
  PhSun,
  PhMoon,
  PhGithubLogo,
  PhTwitterLogo,
  PhSpinner,
  PhGauge,
  PhShield,
  PhDevices,
  PhPalette,
  PhCode,
  PhFileTs,
  PhWind,
  PhAtom,
} from "@phosphor-icons/vue";

const greetMsg = ref("");
const greetResponse = ref("");
const isLoading = ref(false);
const isDark = ref(false);

const stats = {
  appSize: "~3MB",
  memory: "~50MB",
  startup: "<100ms",
};

const features = [
  {
    icon: PhGauge,
    title: "极致性能",
    description: "基于 Rust 构建，内存占用极低，启动速度快如闪电。",
  },
  {
    icon: PhShield,
    title: "安全可靠",
    description: "默认启用前端隔离，安全策略由 Rust 强制实施。",
  },
  {
    icon: PhDevices,
    title: "跨平台",
    description: "一套代码，多端运行。支持 Windows、macOS 和 Linux。",
  },
  {
    icon: PhPalette,
    title: "现代 UI",
    description: "使用 Tailwind CSS 构建响应式界面，支持深色模式。",
  },
];

const techStack = [
  {
    icon: PhAtom,
    name: "Vue 3",
    description: "渐进式框架",
  },
  {
    icon: PhCode,
    name: "Rust",
    description: "系统级性能",
  },
  {
    icon: PhWind,
    name: "Tailwind",
    description: "实用优先 CSS",
  },
  {
    icon: PhFileTs,
    name: "TypeScript",
    description: "类型安全",
  },
];

async function greet() {
  if (!greetMsg.value.trim()) return;
  isLoading.value = true;
  try {
    greetResponse.value = await invoke("greet", { name: greetMsg.value });
  } finally {
    isLoading.value = false;
  }
}

function scrollToDemo() {
  document.getElementById("demo")?.scrollIntoView({ behavior: "smooth" });
}

function toggleTheme() {
  isDark.value = !isDark.value;
  if (isDark.value) {
    document.documentElement.classList.add("dark");
  } else {
    document.documentElement.classList.remove("dark");
  }
}

onMounted(() => {
  if (window.matchMedia("(prefers-color-scheme: dark)").matches) {
    isDark.value = true;
    document.documentElement.classList.add("dark");
  }
});
</script>
