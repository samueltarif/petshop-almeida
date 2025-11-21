<template>
  <section id="servicos">
    <h2>Nossos Serviços</h2>
    <div class="services-grid">
      <ServiceDogWalker />
      <ServiceTaxiDog />
      <ServiceTaxiConsulta />
      <ServiceBanhoTosaHigienica />
      <ServiceSomenteBanho />
      <ServiceBanhoSpitz />
      <ServiceTosaTesoura />
      <ServiceBanhoFelinos />
      <ServiceTosaPadrao />
      <ServiceTosaZero />
      <ServiceRemocaoPeloMorto />
      <ServiceTransformacoes />
    </div>
  </section>
</template>

<script setup lang="ts">
import ServiceDogWalker from '~/components/services/ServiceDogWalker.vue'
import ServiceTaxiDog from '~/components/services/ServiceTaxiDog.vue'
import ServiceTaxiConsulta from '~/components/services/ServiceTaxiConsulta.vue'
import ServiceBanhoTosaHigienica from '~/components/services/ServiceBanhoTosaHigienica.vue'
import ServiceSomenteBanho from '~/components/services/ServiceSomenteBanho.vue'
import ServiceBanhoSpitz from '~/components/services/ServiceBanhoSpitz.vue'
import ServiceTosaTesoura from '~/components/services/ServiceTosaTesoura.vue'
import ServiceBanhoFelinos from '~/components/services/ServiceBanhoFelinos.vue'
import ServiceTosaPadrao from '~/components/services/ServiceTosaPadrao.vue'
import ServiceTosaZero from '~/components/services/ServiceTosaZero.vue'
import ServiceRemocaoPeloMorto from '~/components/services/ServiceRemocaoPeloMorto.vue'
import ServiceTransformacoes from '~/components/services/ServiceTransformacoes.vue'
</script>

<style scoped>
section { padding: 60px var(--space-20); max-width: 1280px; margin: 0 auto; }
section h2 { text-align: center; font-size: var(--font-size-4xl); margin-bottom: var(--space-32); color: var(--pet-primary); font-weight: var(--font-weight-bold); letter-spacing: var(--letter-spacing-tight); }
.services-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: var(--space-24); }
/* estilos de conteúdo movidos para ServiceCard.vue via :deep */
</style>