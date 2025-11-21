<template>
  <button
    class="theme-toggle"
    :aria-pressed="isBlack ? 'true' : 'false'"
    :aria-label="isBlack ? 'Tema black ativado' : 'Tema claro ativado'"
    type="button"
    @click="toggleTheme"
  >
    <span class="icon" aria-hidden="true">
      <!-- Sol para tema claro -->
      <svg v-if="!isBlack" class="icon-sun" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="5" stroke="currentColor" stroke-width="2" />
        <path d="M12 1v3M12 20v3M4.22 4.22l2.12 2.12M17.66 17.66l2.12 2.12M1 12h3M20 12h3M4.22 19.78l2.12-2.12M17.66 6.34l2.12-2.12" stroke="currentColor" stroke-width="2" stroke-linecap="round" />
      </svg>
      <!-- Lua para tema black -->
      <svg v-else class="icon-moon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z" stroke="currentColor" stroke-width="2" fill="none" />
      </svg>
    </span>
  </button>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const isBlack = ref(false)

const applyThemeClass = (active: boolean) => {
  const root = document.documentElement
  if (active) {
    root.classList.add('theme-black')
    root.classList.remove('theme-light')
    localStorage.setItem('theme', 'black')
  } else {
    root.classList.remove('theme-black')
    root.classList.add('theme-light')
    localStorage.setItem('theme', 'default')
  }
}

const toggleTheme = () => {
  isBlack.value = !isBlack.value
  applyThemeClass(isBlack.value)
}

onMounted(() => {
  const saved = localStorage.getItem('theme')
  isBlack.value = saved === 'black'
  applyThemeClass(isBlack.value)
})
</script>

<style scoped>
.theme-toggle {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: transparent;
  border: 1px solid var(--color-card-border);
  color: var(--color-text);
  border-radius: var(--radius-full);
  padding: 8px 12px;
  cursor: pointer;
  box-shadow: var(--shadow-sm);
  transition: border-color var(--duration-fast) var(--ease-standard), transform var(--duration-fast) var(--ease-standard);
}
.theme-toggle:hover { border-color: var(--color-border); transform: translateY(-1px); }
.theme-toggle:focus { outline: none; box-shadow: var(--focus-ring); }

/* Ícone único (sol/lua) */
.icon { display: inline-flex; align-items: center; justify-content: center; }
.icon-sun, .icon-moon { width: 18px; height: 18px; color: var(--color-text); }
</style>