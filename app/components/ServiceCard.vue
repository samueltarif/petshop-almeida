<template>
  <div class="service-card">
    <ServiceIcon :aria-label="ariaLabel">
      <slot name="icon" />
    </ServiceIcon>
    <h3>{{ title }}</h3>
    <div
      v-if="images?.length"
      class="image-gallery"
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
      class="lightbox-overlay"
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
      <button class="lightbox-close" type="button" aria-label="Fechar" @click="closeLightbox">✕</button>
      <div class="lightbox-content">
        <img :src="displayImages[lightboxIndex]" :alt="`Foto ${lightboxIndex + 1}`" class="lightbox-image" />
      </div>
      <button class="lightbox-arrow left" type="button" aria-label="Imagem anterior" @click="prevLB">‹</button>
      <button class="lightbox-arrow right" type="button" aria-label="Próxima imagem" @click="nextLB">›</button>
    </div>
    <slot />
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
}>(), {
  images: ['/images/dog.jpg', '/images/toby.jpg']
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
</script>

<style scoped>
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
</style>