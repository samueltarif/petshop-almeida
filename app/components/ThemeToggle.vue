<template>
  <button
    class="theme-toggle"
    :aria-pressed="isBlack ? 'true' : 'false'"
    :aria-label="isBlack ? 'Tema preto ativado' : 'Ativar tema preto'"
    type="button"
    @click="toggleTheme"
  >
    <span class="icon-desktop" aria-hidden="true">
      <span class="badge">
        <span class="shine"></span>
      </span>
      <span class="label">Tema</span>
    </span>
    <span class="icon-mobile" aria-hidden="true">
      <span class="dot"></span>
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
    localStorage.setItem('theme', 'black')
  } else {
    root.classList.remove('theme-black')
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

/* Desktop icon */
.icon-desktop { display: inline-flex; align-items: center; gap: 10px; }
.badge {
  width: 22px;
  height: 22px;
  border-radius: 6px;
  background: linear-gradient(135deg, #121416 0%, #0d0f12 60%, #0a0c0f 100%);
  border: 1px solid rgba(255,255,255,0.08);
  box-shadow: inset 0 1px 2px rgba(255,255,255,0.1), inset 0 -2px 2px rgba(0,0,0,0.25), 0 2px 4px rgba(0,0,0,0.25);
  position: relative;
}
.shine { position: absolute; inset: 0; background: linear-gradient(180deg, rgba(255,255,255,0.12), rgba(255,255,255,0)); border-radius: 6px; }
.label { font-size: var(--font-size-base); font-weight: var(--font-weight-medium); }

/* Mobile icon */
.icon-mobile { display: none; }
.dot {
  width: 16px;
  height: 16px;
  border-radius: var(--radius-full);
  background: radial-gradient(circle at 30% 30%, #0f1113 0%, #0a0c0f 60%, #07090b 100%);
  border: 1px solid rgba(255,255,255,0.08);
  box-shadow: inset 0 2px 2px rgba(255,255,255,0.1), inset 0 -2px 2px rgba(0,0,0,0.25), 0 2px 4px rgba(0,0,0,0.25);
}

/* Responsivo: alterna visual desktop/mobile */
@media (max-width: 768px) {
  .icon-desktop { display: none; }
  .icon-mobile { display: inline-flex; }
}
</style>