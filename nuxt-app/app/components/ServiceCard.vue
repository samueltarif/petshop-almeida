<template>
  <div class="service-card bg-[var(--color-surface)] border border-[var(--color-card-border)] rounded-lg p-6 shadow-sm transition-transform duration-300 hover:-translate-y-0.5 hover:shadow-lg">
    <ServiceIcon :aria-label="ariaLabel" class="mb-3">
      <slot name="icon" />
    </ServiceIcon>
    <h3 class="text-[var(--pet-primary)] text-xl font-semibold tracking-tight mb-3 neon-title">{{ title }}</h3>
    <div
      v-if="images?.length"
      class="image-gallery my-4 rounded-md overflow-hidden bg-[var(--color-bg-1)]"
      role="region"
      aria-label="Galeria de imagens"
      @touchstart="onTouchStart"
      @touchmove="onTouchMove"
      @touchend="onTouchEnd"
      @touchcancel="onTouchEnd"
    >
      <div class="gallery-track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <div
          v-for="(src, i) in displayImages"
          :key="i"
          class="image-frame"
          :style="i === currentIndex ? { transform: `scale(${zoomScale})` } : {}"
        >
          <img :src="src" :alt="`Foto ${i + 1}`" loading="lazy" @error="onImageError(i)" @click="openLightbox(i)" />
        </div>
      </div>
      <button class="arrow left" type="button" aria-label="Imagem anterior" @click="prev">‹</button>
      <button class="arrow right" type="button" aria-label="Próxima imagem" @click="next">›</button>
    </div>

    <!-- Lightbox overlay -->
    <div
      v-if="lightboxOpen"
      class="lightbox-overlay fixed inset-0 bg-black/80 flex items-center justify-center z-[1000]"
      role="dialog"
      aria-modal="true"
      aria-label="Visualização de imagem"
      tabindex="0"
      @keydown.stop="onKeydown"
      @click.self="closeLightbox"
      @touchstart="onLBTouchStart"
      @touchmove="onLBTouchMove"
      @touchend="onLBTouchEnd"
      @touchcancel="onLBTouchEnd"
    >
      <button class="lightbox-close absolute top-3 right-3 bg-black/50 text-white w-9 h-9 rounded-full" type="button" aria-label="Fechar" @click="closeLightbox">✕</button>
      <div class="lightbox-content max-w-[90vw] max-h-[85vh]">
        <img :src="displayImages[lightboxIndex]" :alt="`Foto ${lightboxIndex + 1}`" class="lightbox-image max-w-full max-h-[85vh] object-contain rounded-md" />
      </div>
      <button class="lightbox-arrow left absolute top-1/2 -translate-y-1/2 bg-white/20 text-white w-11 h-11 rounded-full flex items-center justify-center" type="button" aria-label="Imagem anterior" @click="prevLB">‹</button>
      <button class="lightbox-arrow right absolute top-1/2 -translate-y-1/2 bg-white/20 text-white w-11 h-11 rounded-full flex items-center justify-center" type="button" aria-label="Próxima imagem" @click="nextLB">›</button>
    </div>
    <slot />

<button
      v-if="showExtras"
      class="additional-services mt-4 flex items-center gap-2 group"
      type="button"
      aria-label="Abrir serviços adicionais"
      aria-haspopup="dialog"
      aria-controls="extras-modal"
      @click="openExtras"
    >
      <svg class="plus-icon w-6 h-6" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <defs>
          <linearGradient id="plus-grad" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#5ab0ff" />
            <stop offset="100%" stop-color="#1470c9" />
          </linearGradient>
          <linearGradient id="plus-edge" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0%" stop-color="#ffffff" stop-opacity="0.85" />
            <stop offset="100%" stop-color="#ffffff" stop-opacity="0" />
          </linearGradient>
          <filter id="plus-shadow" x="-20%" y="-20%" width="140%" height="140%">
            <feDropShadow dx="0" dy="3" stdDeviation="3" flood-color="#000000" flood-opacity="0.35" />
          </filter>
        </defs>
        <g filter="url(#plus-shadow)">
          <g transform="translate(2,2)">
            <rect x="28" y="10" width="8" height="44" rx="4" fill="#0b2a3a" />
            <rect x="10" y="28" width="44" height="8" rx="4" fill="#0b2a3a" />
          </g>
          <g>
            <rect x="28" y="10" width="8" height="44" rx="4" fill="url(#plus-grad)" />
            <rect x="10" y="28" width="44" height="8" rx="4" fill="url(#plus-grad)" />
            <rect x="28" y="10" width="8" height="44" rx="4" fill="url(#plus-edge)" opacity="0.6" />
            <rect x="10" y="28" width="44" height="8" rx="4" fill="url(#plus-edge)" opacity="0.6" />
          </g>
          <animateTransform attributeName="transform" type="rotate" from="0 32 32" to="360 32 32" dur="8s" repeatCount="indefinite" />
        </g>
      </svg>
      <span class="label text-[var(--color-text)] font-medium group-hover:text-[var(--pet-primary)]">Serviços Adicionais</span>
    </button>

    <!-- Popup de Serviços Adicionais (Teleport para body) -->
    <Teleport to="body">
      <div
        v-if="showExtras && extrasOpen"
        id="extras-modal"
        class="extras-overlay fixed inset-0 bg-black/70 flex items-center justify-center z-[10000]"
        role="dialog"
        aria-modal="true"
        aria-label="Serviços Adicionais"
        tabindex="0"
        @keydown.stop="onExtrasKeydown"
        @click.self="closeExtras"
      >
        <div class="extras-content relative bg-[var(--color-surface)] border border-[var(--color-card-border)] rounded-lg p-6 shadow-xl w-[min(90vw,560px)]">
          <button class="extras-close absolute top-3 right-3 bg-black/50 text-white w-9 h-9 rounded-full" type="button" aria-label="Fechar" @click="closeExtras">✕</button>
          <div class="extras-header flex items-center gap-3 mb-4">
            <svg class="w-8 h-8" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
              <defs>
                <linearGradient id="plus-grad-popup" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="0%" stop-color="#5ab0ff" />
                  <stop offset="100%" stop-color="#1470c9" />
                </linearGradient>
                <filter id="plus-shadow-popup" x="-20%" y="-20%" width="140%" height="140%">
                  <feDropShadow dx="0" dy="3" stdDeviation="3" flood-color="#000000" flood-opacity="0.35" />
                </filter>
              </defs>
              <g filter="url(#plus-shadow-popup)">
                <g transform="translate(2,2)">
                  <rect x="28" y="10" width="8" height="44" rx="4" fill="#0b2a3a" />
                  <rect x="10" y="28" width="44" height="8" rx="4" fill="#0b2a3a" />
                </g>
                <g>
                  <rect x="28" y="10" width="8" height="44" rx="4" fill="url(#plus-grad-popup)" />
                  <rect x="10" y="28" width="44" height="8" rx="4" fill="url(#plus-grad-popup)" />
                </g>
                <animateTransform attributeName="transform" type="rotate" from="0 32 32" to="360 32 32" dur="10s" repeatCount="indefinite" />
              </g>
            </svg>
            <h4 class="text-[var(--color-text)] text-lg font-semibold">Serviços Adicionais</h4>
          </div>
          <div class="extras-body text-[var(--color-text)]">
            <ul class="list-disc ml-5 space-y-2">
              <li v-for="(item, i) in extrasItems" :key="i">{{ item }}</li>
            </ul>
          </div>
        </div>
      </div>
    </Teleport>
  </div>
</template>

<script setup lang="ts">
import ServiceIcon from './ServiceIcon.vue'
import { ref, computed, watch } from 'vue'
import { useRuntimeConfig } from '#imports'

const props = withDefaults(defineProps<{
  title: string
  ariaLabel?: string
  images?: string[]
  showExtras?: boolean
  extrasItems?: string[]
}>(), {
  images: ['/images/dog.jpg', '/images/toby.jpg'],
  showExtras: true,
  extrasItems: [
    'Coloração – a partir de R$15,00',
    'Desembolo – R$30,00 a hora',
    'Corte de unha – R$10,00',
    'Hidratação – R$20,00',
    'Higiene bucal – R$10,00'
  ]
})

const currentIndex = ref(0)
const appBase = useRuntimeConfig()?.app?.baseURL || '/'
const resolvedImages = computed(() => (props.images || []).map((src) => {
  // Mantém URLs absolutas (http/https) como estão
  if (/^https?:\/\//.test(src)) return src
  const clean = src.startsWith('/') ? src.slice(1) : src
  return appBase.replace(/\/$/, '/') + clean
}))

// Array mutável de exibição com fallback
const displayImages = ref<string[]>([])
watch(resolvedImages, (val) => { displayImages.value = [...val] }, { immediate: true })
const onImageError = (i: number) => {
  // Fallback para imagem local
  displayImages.value[i] = appBase.replace(/\/$/, '/') + 'images/dog.jpg'
}
const next = () => {
  if (!props.images?.length) return
  currentIndex.value = (currentIndex.value + 1) % props.images.length
}
const prev = () => {
  if (!props.images?.length) return
  currentIndex.value = (currentIndex.value - 1 + props.images.length) % props.images.length
}

// Pinch-to-zoom para mobile
const zoomScale = ref(1)
let startDist = 0
let startScale = 1
const getDist = (touches: TouchList) => {
  const [a, b] = [touches[0], touches[1]]
  const dx = a.clientX - b.clientX
  const dy = a.clientY - b.clientY
  return Math.sqrt(dx * dx + dy * dy)
}
const clamp = (n: number, min = 1, max = 3) => Math.max(min, Math.min(max, n))
const onTouchStart = (e: TouchEvent) => {
  if (e.touches.length === 2) {
    startDist = getDist(e.touches)
    startScale = zoomScale.value
  }
}
const onTouchMove = (e: TouchEvent) => {
  if (e.touches.length === 2 && startDist) {
    const d = getDist(e.touches)
    zoomScale.value = clamp(startScale * (d / startDist))
    e.preventDefault()
  }
}
const onTouchEnd = () => {
  if (zoomScale.value < 1.02) zoomScale.value = 1
}

// Lightbox state & handlers
const lightboxOpen = ref(false)
const lightboxIndex = ref(0)
const openLightbox = (i: number) => { lightboxIndex.value = i; lightboxOpen.value = true }
const closeLightbox = () => { lightboxOpen.value = false }
const nextLB = () => { lightboxIndex.value = (lightboxIndex.value + 1) % displayImages.value.length }
const prevLB = () => { lightboxIndex.value = (lightboxIndex.value - 1 + displayImages.value.length) % displayImages.value.length }
const onKeydown = (e: KeyboardEvent) => {
  if (e.key === 'Escape') return closeLightbox()
  if (e.key === 'ArrowRight') return nextLB()
  if (e.key === 'ArrowLeft') return prevLB()
}
// Swipe navigation for lightbox
let lbStartX = 0
let lbMoveX = 0
const onLBTouchStart = (e: TouchEvent) => { lbStartX = e.touches[0].clientX; lbMoveX = lbStartX }
const onLBTouchMove = (e: TouchEvent) => { lbMoveX = e.touches[0].clientX }
const onLBTouchEnd = () => {
  const delta = lbMoveX - lbStartX
  const threshold = 40
  if (Math.abs(delta) > threshold) { delta < 0 ? nextLB() : prevLB() }
  lbStartX = 0; lbMoveX = 0
}

// Extras popup state & handlers
const extrasOpen = ref(false)
const openExtras = (e?: Event) => { if (e) e.stopPropagation(); extrasOpen.value = true }
const closeExtras = () => { extrasOpen.value = false }
const onExtrasKeydown = (e: KeyboardEvent) => { if (e.key === 'Escape') closeExtras() }
</script>

<style scoped>
.service-card { position: relative; }

/* Anel de brilho neon azul no contorno do card */
 

 

/* Título com contorno/efeito neon azul */
.neon-title { text-shadow: none; -webkit-text-stroke: 0; }

.image-gallery {
  position: relative;
  margin: var(--space-16) 0;
  border-radius: var(--radius-md);
  overflow: hidden;
  background: var(--color-bg-1);
}

.gallery-track {
  display: flex;
  width: 100%;
  transition: transform var(--duration-normal) var(--ease-standard);
}

.gallery-track img {
  width: 100%;
  height: 220px;
  object-fit: cover;
  flex-shrink: 0;
}

.image-frame {
  width: 100%;
  height: 220px;
  overflow: hidden;
  will-change: transform;
  flex: 0 0 100%; /* impede encolhimento e garante uma imagem por "página" */
}

.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0,0,0,0.4);
  color: #fff;
  border: none;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  backdrop-filter: blur(2px);
}

.arrow.left { left: 8px; }
.arrow.right { right: 8px; }

.arrow:hover { background: rgba(0,0,0,0.6); }

/* Lightbox styles */
.lightbox-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}
.lightbox-content {
  max-width: 90vw;
  max-height: 85vh;
}
.lightbox-image {
  max-width: 100%;
  max-height: 85vh;
  object-fit: contain;
  border-radius: var(--radius-md);
}
.lightbox-close {
  position: absolute;
  top: 12px;
  right: 12px;
  background: rgba(0,0,0,0.5);
  color: #fff;
  border: none;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  cursor: pointer;
}
.lightbox-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255,255,255,0.2);
  color: #fff;
  border: none;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
.lightbox-arrow.left { left: 16px; }
.lightbox-arrow.right { right: 16px; }

.additional-services {
  color: var(--color-text);
  background: transparent;
  border: 1px solid var(--color-card-border);
  padding: var(--space-8) var(--space-12);
  border-radius: var(--radius-md);
  transition: all var(--duration-normal) var(--ease-standard);
}
.plus-icon {
  display: inline-block;
}
.additional-services:hover { border-color: var(--pet-primary); transform: translateY(-1px); box-shadow: var(--shadow-sm); }

/* Extras popup */
.extras-overlay { z-index: 10000; }
.extras-content { box-shadow: var(--shadow-lg); }
.extras-close:hover { background: rgba(0,0,0,0.65); }

/* Conteúdo comum dos cards de serviço (aplica aos elementos vindos via slot) */
:deep(.service-description) { color: var(--color-text-secondary); margin-bottom: var(--space-16); font-size: var(--font-size-base); }
:deep(.service-note) { background: var(--color-bg-3); color: var(--color-text); padding: var(--space-8) var(--space-12); border-radius: var(--radius-base); font-size: var(--font-size-sm); font-weight: var(--font-weight-medium); margin-bottom: var(--space-16); border: 1px solid var(--color-card-border); }
:deep(.service-availability) { background: #FFD700; color: #111; padding: var(--space-6) var(--space-12); border-radius: var(--radius-base); font-size: var(--font-size-sm); font-weight: var(--font-weight-semibold); display: inline-block; margin-bottom: var(--space-16); position: relative; border: 1px solid #111; }
/* tabela de preços comum aos serviços */
:deep(.price-table) { width: 100%; border-collapse: collapse; margin-top: var(--space-12); }
:deep(.price-table th), :deep(.price-table td) { text-align: left; padding: var(--space-8) var(--space-12); border-bottom: 1px solid var(--color-border); font-size: var(--font-size-sm); }
:deep(.price-table thead th) { color: var(--color-text-secondary); font-weight: var(--font-weight-semibold); }
:deep(.price-table tbody tr:hover) { background: var(--color-bg-hover); }

/* lista de itens comum aos serviços */
:deep(.service-list) { list-style: none; margin-top: var(--space-12); }
:deep(.service-list li) { padding: var(--space-8) 0; padding-left: var(--space-24); position: relative; font-size: var(--font-size-base); }
:deep(.service-list li)::before { content: '✓'; position: absolute; left: 0; color: var(--pet-primary); font-weight: var(--font-weight-bold); }
</style>
