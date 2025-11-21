<template>
  <header>
    <div class="header-container">
      <div class="logo"><AnimePaw :size="26" /><AnimePaw :size="26" /> Pets Almeida</div>
      <div class="header-right">
        <ThemeToggle />
        <NavMenu id="mainNav" :items="navItems" :active="isNavActive" @click-link="isNavActive = false" />
        <MenuToggle :active="isNavActive" @toggle="isNavActive = !isNavActive" />
      </div>
      <div v-if="isNavActive" class="nav-backdrop" @click="isNavActive = false" aria-hidden="true" />
    </div>
  </header>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import AnimePaw from '~/components/AnimePaw.vue'
import ThemeToggle from '~/components/ThemeToggle.vue'
import MenuToggle from '~/components/MenuToggle.vue'
import NavMenu from '~/components/NavMenu.vue'

const props = defineProps<{ navItems: { label: string; href: string }[] }>()
const isNavActive = ref(false)
const navItems = props.navItems
</script>

<style scoped>
header { position: sticky; top: 0; background: var(--color-surface); box-shadow: var(--shadow-sm); z-index: 1000; border-bottom: 1px solid var(--color-card-border); }
.header-container { max-width: 1280px; margin: 0 auto; padding: var(--space-16) var(--space-20); display: flex; justify-content: space-between; align-items: center; }
.header-right { display: flex; align-items: center; gap: var(--space-12); }
.logo { font-size: var(--font-size-3xl); font-weight: var(--font-weight-bold); color: var(--pet-primary); display: flex; align-items: center; gap: var(--space-8); }
/* Desktop nav (alcança conteúdo do NavMenu) */
:deep(nav ul) { display: flex; list-style: none; gap: var(--space-24); }
:deep(nav a) { color: var(--color-text); text-decoration: none; font-weight: var(--font-weight-medium); transition: color var(--duration-fast) var(--ease-standard); font-size: var(--font-size-base); }
:deep(nav a:hover) { color: var(--pet-primary); }
.menu-toggle { display: inline-flex; background: none; border: none; font-size: 28px; cursor: pointer; color: var(--color-text); }

/* Mobile nav */
@media (max-width: 768px) {
  .menu-toggle { display: inline-flex; }
  .header-container { display: flex; flex-direction: row; align-items: center; justify-content: space-between; gap: var(--space-12); flex-wrap: nowrap; }
  .logo { flex: 1 1 auto; }
  :deep(.theme-toggle), .menu-toggle { flex: 0 0 auto; display: inline-flex; align-items: center; }
  /* Backdrop abaixo do header, acima do conteúdo */
  .nav-backdrop { position: fixed; inset: 0; top: 70px; background: rgba(0,0,0,0.45); z-index: 999; }
  :deep(nav) { position: fixed; top: 70px; left: 0; width: 100%; background: var(--color-surface); padding: var(--space-24); box-shadow: var(--shadow-lg); border-bottom: 1px solid var(--color-card-border); z-index: 1000; transform: translateX(-100%); transition: transform var(--duration-normal) var(--ease-standard); }
  :deep(nav.active) { transform: translateX(0); }
  :deep(nav ul) { flex-direction: column; gap: var(--space-16); }
  :deep(nav a) { font-size: var(--font-size-lg); display: block; padding: var(--space-12); }
}
</style>
