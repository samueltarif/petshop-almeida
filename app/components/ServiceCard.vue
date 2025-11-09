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
          <img :src="src" :alt="`Foto ${i + 1}`" loading="lazy" @error="onImageError(i)" />
        </div>
      </div>
      <button class="arrow left" type="button" aria-label="Imagem anterior" @click="prev">‹</button>
      <button class="arrow right" type="button" aria-label="Próxima imagem" @click="next">›</button>
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
</style>