<template>
  <div class="service-card">
    <ServiceIcon :aria-label="ariaLabel">
      <slot name="icon" />
    </ServiceIcon>
    <h3>{{ title }}</h3>
    <div v-if="images?.length" class="image-gallery" role="region" aria-label="Galeria de imagens">
      <div class="gallery-track" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <img v-for="(src, i) in images" :key="i" :src="src" :alt="`Foto ${i + 1}`" loading="lazy" />
      </div>
      <button class="arrow left" type="button" aria-label="Imagem anterior" @click="prev">‹</button>
      <button class="arrow right" type="button" aria-label="Próxima imagem" @click="next">›</button>
    </div>
    <slot />
  </div>
</template>

<script setup lang="ts">
import ServiceIcon from './ServiceIcon.vue'
import { ref } from 'vue'

const props = withDefaults(defineProps<{
  title: string
  ariaLabel?: string
  images?: string[]
}>(), {
  images: ['/images/dog.jpg', '/images/toby.jpg']
})

const currentIndex = ref(0)
const next = () => {
  if (!props.images?.length) return
  currentIndex.value = (currentIndex.value + 1) % props.images.length
}
const prev = () => {
  if (!props.images?.length) return
  currentIndex.value = (currentIndex.value - 1 + props.images.length) % props.images.length
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