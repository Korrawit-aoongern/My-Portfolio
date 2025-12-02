<script setup>
import { ref, onMounted } from "vue"


const theme = ref(localStorage.getItem("theme") || "system")

const applyTheme = () => {
  const root = document.documentElement

  if (theme.value === "light") {
    root.classList.remove("dark")
    localStorage.setItem("theme", "light")
  } else if (theme.value === "dark") {
    root.classList.add("dark")
    localStorage.setItem("theme", "dark")
  } else {
    // System mode
    localStorage.removeItem("theme")
    const systemPrefersDark = window.matchMedia("(prefers-color-scheme: dark)").matches
    root.classList.toggle("dark", systemPrefersDark)
  }
}

// Detect changes to OS theme when in system mode
const systemWatcher = window.matchMedia("(prefers-color-scheme: dark)")
systemWatcher.addEventListener("change", () => {
  if (theme.value === "system") applyTheme()
})

onMounted(() => {
  applyTheme()
})

const cycleTheme = () => {
  if (theme.value === "light") theme.value = "dark"
  else if (theme.value === "dark") theme.value = "system"
  else theme.value = "light"

  applyTheme()
}

const currentLang = ref("TH")

function toggleLang() {
  currentLang.value = currentLang.value === "TH" ? "EN" : "TH"
}
</script>

<template>
  <div class="min-h-screen bg-neutral-50 text-neutral-900 dark:bg-neutral-900 dark:text-neutral-50 transition-colors ">
    <!-- Navbar -->
    <header class="w-full flex justify-between items-center bg-neutral-50 dark:bg-neutral-900 px-6 py-4 border-b border-neutral-200 dark:border-neutral-700 sticky top-0">
      <h1 class="text-2xl font-bold text-orange-500">Yuzu Portfolio</h1>
      <div class="flex gap-4">
        <!-- Dark mode toggle -->
        <button 
          @click="cycleTheme" 
          class="p-2 rounded-full hover:bg-neutral-200 dark:hover:bg-neutral-700"
        >
          <span v-if="theme === 'light'" class="pi pi-sun"></span>
          <span v-else-if="theme === 'dark'" class="pi pi-moon"></span>
          <span v-else class="pi pi-desktop"></span>
        </button>
        <!-- Language toggle -->
        <button
          @click="toggleLang"
          class="p-2 rounded-full hover:bg-neutral-200 dark:hover:bg-neutral-700 font-semibold"
        >
          <span>{{ currentLang }}</span>
        </button>
      </div>
    </header>

    <!-- Content Wrapper -->
    <main class="px-6 py-10 max-w-4xl mx-auto flex flex-col gap-24">

      <!-- About Me -->
      <section id="about" class="space-y-4">
        <h2 class="text-3xl font-semibold text-orange-500">About Me</h2>
        <p class="text-neutral-700 dark:text-neutral-300">Write something about yourself here...</p>
      </section>

      <!-- Education -->
      <section id="education" class="space-y-4">
        <h2 class="text-3xl font-semibold text-orange-500">Education</h2>
        <div class="space-y-2">
          <div class="p-4 border border-neutral-300 dark:border-neutral-700 rounded-xl">
            <p class="font-semibold">Institution Name</p>
            <p class="text-sm opacity-80">Years and description...</p>
          </div>
        </div>
      </section>

      <!-- Skills -->
      <section id="skills" class="space-y-4">
        <h2 class="text-3xl font-semibold text-orange-500">Skills</h2>
        <div class="grid grid-cols-2 sm:grid-cols-3 gap-4">
          <div class="p-3 border border-neutral-300 dark:border-neutral-700 rounded-lg text-center">Skill A</div>
          <div class="p-3 border border-neutral-300 dark:border-neutral-700 rounded-lg text-center">Skill B</div>
        </div>
      </section>

      <!-- Projects -->
      <section id="projects" class="space-y-4">
        <h2 class="text-3xl font-semibold text-orange-500">Projects</h2>
        <div class="space-y-4">
          <div class="p-4 border border-neutral-300 dark:border-neutral-700 rounded-xl">
            <p class="font-semibold">Project Title</p>
            <p class="text-sm opacity-80">Short description of your project...</p>
          </div>
        </div>
      </section>

      <!-- Timeline of Learning -->
      <section id="timeline" class="space-y-4">
        <h2 class="text-3xl font-semibold text-orange-500">Timeline of Learning</h2>
        <ul class="border-l-2 border-orange-500 pl-4 space-y-4">
          <li>
            <p class="font-semibold">2024</p>
            <p class="text-sm opacity-80">Something you learned...</p>
          </li>
        </ul>
      </section>

      <!-- DevOps Journey -->
      <section id="devops" class="space-y-4">
        <h2 class="text-3xl font-semibold text-orange-500">DevOps Journey</h2>
        <p class="text-neutral-700 dark:text-neutral-300">Write about your pipeline adventures...</p>
      </section>

      <!-- Blog Diary -->
      <section id="blog" class="space-y-4 pb-16">
        <h2 class="text-3xl font-semibold text-orange-500">Blog Diary</h2>
        <div class="space-y-4">
          <article class="p-4 border border-neutral-300 dark:border-neutral-700 rounded-xl">
            <p class="font-semibold">Entry Title</p>
            <p class="text-sm opacity-80">Preview text of your diary...</p>
          </article>
        </div>
      </section>
    </main>
  </div>
</template>

