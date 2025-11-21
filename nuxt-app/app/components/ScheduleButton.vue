<template>
  <div class="relative inline-block">
    <button
      type="button"
      class="inline-flex items-center gap-2 px-2 py-1 text-xs font-semibold rounded-md border transition-colors duration-200"
      :aria-label="`Agendar ${serviceLabel}`"
      data-testid="schedule-button"
      @click="onClick"
    >
      Agendar
    </button>

    <div v-if="showModal" class="extras-overlay fixed inset-0 bg-black/60 flex items-center justify-center z-[10000]" role="dialog" aria-modal="true" aria-label="Serviços adicionais">
      <div class="extras-content relative bg-[var(--color-surface)] border border-[var(--color-card-border)] rounded-lg p-4 w-[min(90vw,420px)] text-sm text-[var(--color-text)]">
        <button type="button" class="extras-close absolute top-2 right-2 w-8 h-8 rounded-full bg-black/50 text-white" aria-label="Fechar" @click="closeModal">✕</button>
        <h3 class="text-base font-semibold mb-2 text-[var(--color-text)]">Gostaria de adicionar mais algum serviço?</h3>
        <p class="text-xs text-[var(--color-text-secondary)] mb-3">Selecione um ou mais extras opcionais para incluir no agendamento.</p>

        <div class="space-y-2 max-h-[40vh] overflow-auto mb-4">
          <label v-for="(item, i) in extras" :key="item" class="extras-item cursor-pointer text-[var(--color-text)]">
            <input type="checkbox" name="extra" :value="item" v-model="selectedExtras" :style="{ accentColor: 'var(--pet-primary)' }">
            <span>{{ item }}</span>
            <span class="image-cell" aria-hidden="true" v-show="!iconsHidden">
              <span v-if="i === 0" class="arrow-down"></span>
              <Image3DIcon
                :size="18"
                aria-label="Ícone de imagem"
                :popup-aria-label="item.includes('Hidratação') ? 'Fotos de Hidratação' : 'Janela de ajuda'"
                :images="item.includes('Hidratação') ? hidrataImages : undefined"
                @open="iconsHidden = true"
                @close="iconsHidden = false"
              />
            </span>
          </label>
        </div>

        <div class="flex gap-2 justify-end">
          <button type="button" class="px-3 py-1 rounded-md border text-xs" @click="schedule(false)">Agendar sem extras</button>
          <button type="button" class="px-3 py-1 rounded-md bg-[#25D366] text-white text-xs disabled:opacity-60" :disabled="!hasRealExtras" @click="schedule(true)">Agendar com extras</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import Image3DIcon from './Image3DIcon.vue'

const props = withDefaults(defineProps<{
  service: string
  variant?: string
  price?: string
  phone?: string
  extras?: string[]
  greetingPrefix?: string
}>(), {
  phone: '5511993602794',
  extras: () => [],
  greetingPrefix: ''
})

const showModal = ref(false)
const selectedExtras = ref<string[]>([])
const iconsHidden = ref(false)
const hidrataImages = ['/images/hidratação.jpg', '/images/hidratação1.jpg', '/images/Hidratação2.jpg']
const hasExtras = computed(() => (props.extras?.length || 0) > 0)
const hasRealExtras = computed(() => selectedExtras.value.length > 0)

// Util: extrair valor em R$ de textos como "Hidratação – R$ 20,00" ou "a partir de R$15,00"
const parseCurrencyBr = (text: string): number | null => {
  const m = text.match(/R\$\s*([0-9]{1,3}(?:\.[0-9]{3})*(?:,[0-9]{2})|[0-9]+(?:,[0-9]{2})?)/)
  if (!m) return null
  const br = m[1]
  // remover pontos de milhar e trocar vírgula por ponto
  const normalized = br.replace(/\./g, '').replace(',', '.')
  const n = parseFloat(normalized)
  return isNaN(n) ? null : n
}
const formatCurrencyBr = (n: number) => n.toLocaleString('pt-BR', { style: 'currency', currency: 'BRL' })
const extrasTotal = computed(() => selectedExtras.value.reduce((sum, item) => {
  const v = parseCurrencyBr(item)
  return sum + (v ?? 0)
}, 0))

const serviceLabel = computed(() => [props.service, props.variant, props.price].filter(Boolean).join(' – '))

const buildWhatsUrl = (includeExtra: boolean) => {
  const base = `https://wa.me/${props.phone}`
  const prefix = props.greetingPrefix ? `${props.greetingPrefix}. ` : 'Olá! '

  const lines: string[] = []
  lines.push(`${prefix}📅 Gostaria de agendar ${serviceLabel.value}.`)

  if (includeExtra && hasRealExtras.value) {
    lines.push('🧩 Extras selecionados:')
    for (const item of selectedExtras.value) {
      lines.push(`• ${item} ✅`)
    }
    if (extrasTotal.value > 0) {
      lines.push(`\n💰 Total dos extras: ${formatCurrencyBr(extrasTotal.value)}`)
    }

    // Mensagem especial para itens sem preço
    const missing = selectedExtras.value.filter((item) => parseCurrencyBr(item) == null)
    if (missing.length > 0) {
      const nomes = missing.map(n => `'${n}'`).join(', ')
      const phrase = props.greetingPrefix
        ? `No site não há informações de preço para este(s) serviço(s) ${nomes} e tenho interesse em agendar, poderia me ajudar?`
        : `Olá, vim do seu site, e no site nao tem informações de preço para este tipo de serviço ${nomes} e tenho interesse em agendar, poderia me ajudar?`
      lines.push(`\nℹ️ ${phrase}`)
    }
  }

  // Total geral com serviço principal caso tenha preço
  const servicePriceText = props.price ?? serviceLabel.value
  const servicePrice = parseCurrencyBr(servicePriceText)
  if (servicePrice != null && (servicePrice > 0 || extrasTotal.value > 0)) {
    const grandTotal = servicePrice + extrasTotal.value
    lines.push(`\n💵 Total geral (serviço + extras): ${formatCurrencyBr(grandTotal)}`)
  }

  lines.push('\nPor favor, poderia confirmar a disponibilidade? Obrigado! 🙏')

  const q = encodeURIComponent(lines.join('\n'))
  return `${base}?text=${q}`
}

const onClick = (e: Event) => {
  e.preventDefault()
  if (hasExtras.value) {
    showModal.value = true
  } else {
    schedule(false)
  }
}

const closeModal = () => { showModal.value = false }
const schedule = (includeExtra: boolean) => {
  const url = buildWhatsUrl(includeExtra)
  const win = window.open(url, '_blank')
  if (!win || win.closed || typeof win.closed === 'undefined') {
    const fallback = document.createElement('div')
    fallback.setAttribute('role', 'alert')
    fallback.setAttribute('aria-live', 'assertive')
    fallback.textContent = 'Não foi possível abrir o WhatsApp. Redirecionando…'
    fallback.className = 'sr-only'
    document.body.appendChild(fallback)
    window.location.href = url
  }
  closeModal()
}
</script>

<style scoped>
button { border-color: var(--color-card-border); color: var(--color-text); background: transparent; }
button:hover { border-color: var(--pet-primary); color: var(--pet-primary); }
.extras-overlay { z-index: 10000; }
.extras-content { box-shadow: var(--shadow-lg); }
.extras-close:hover { background: rgba(0,0,0,0.2); }

@media (prefers-reduced-motion: reduce) {}

.extras-item { display: grid; grid-template-columns: auto 1fr 18px; align-items: center; column-gap: 8px; width: 100%; }
.extras-item > .image-cell { justify-self: end; position: relative; width: 18px; height: 18px; overflow: visible; z-index: 2; }
.arrow-down { position: absolute; left: 50%; transform: translateX(-50%); top: -16px; width: 0; height: 0; border-left: 8px solid transparent; border-right: 8px solid transparent; border-top: 12px solid var(--pet-primary); filter: drop-shadow(0 1px 1px rgba(0,0,0,0.3)); animation: nudge 1.6s ease-in-out infinite; }
@keyframes nudge { 0%, 100% { transform: translateX(-50%) translateY(0); } 50% { transform: translateX(-50%) translateY(2px); } }
</style>
