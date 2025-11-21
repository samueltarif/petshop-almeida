<template>
  <div>
    <HeaderBar :navItems="navItems" />

    <section class="hero" id="home">
      <div class="hero-content">
        <h1><AnimePaw :size="34" /><AnimePaw :size="34" /> Pets Almeida</h1>
        <p class="tagline">Cuidado e carinho para seu pet <Heart3DIcon :size="22" /></p>
        <p class="welcome">
          Bem-vindo ao Pets Almeida! Somos especializados em banho, tosa e táxi dog em São Paulo.
          Tratamos seu pet com todo amor e profissionalismo que ele merece.
        </p>
        <div class="hero-cta">
          <AgendeAgoraButton />
          
          
        </div>
      </div>
      <!-- Paws overlay, absoluto e atrás do conteúdo -->
      <ClientOnly>
        <HeroPaws
          :count="28"
          color="#000000"
          :minSize="18"
          :maxSize="42"
          :speed="16"
          :opacityMin="0.10"
          :opacityMax="0.18"
        />
      </ClientOnly>
    </section>

    <section id="sobre">
      <h2>Sobre Nós</h2>
      <div class="about-content">
        <p>
          O Pets Almeida é referência em cuidados para pets na região do Limão, São Paulo.
          Com profissionais experientes e apaixonados por animais, oferecemos serviços de
          banho, tosa e táxi dog com qualidade e dedicação.
        </p>
        <p>
          Nossa missão é proporcionar bem-estar e conforto para seu melhor amigo,
          com atendimento personalizado e todo o carinho que ele merece.
        </p>
        <div class="highlights">
          <div class="highlight-item">
            <ThreeDIcon />
            <h3>Profissionais Experientes</h3>
            <p>Equipe qualificada e treinada</p>
          </div>
          <div class="highlight-item">
            <CarTaxi3DIcon />
            <h3>Táxi Dog</h3>
            <p>Transporte seguro para seu pet</p>
          </div>
          <div class="highlight-item">
  <div class="icon" aria-label="Ícone de localização"><Location3DIcon /></div>
            <h3>Localização</h3>
            <p>Av. Inajar de Souza, 3823<br>Limão - São Paulo</p>
          </div>
        </div>
      </div>
    </section>

    <ServicesSection />

    <PaymentsSection />

    <ContactSection />

    <div v-if="termsOpen" class="terms-overlay" role="dialog" aria-modal="true" aria-labelledby="terms-title">
      <div class="terms-dialog">
        <div class="terms-header">
          <h2 id="terms-title">Termos de Uso</h2>
          <button class="terms-close" type="button" @click="termsOpen = false" aria-label="Fechar Termos">Fechar</button>
        </div>
        <div class="terms-content">
          <p>
            Ao utilizar o site e os serviços do Pets Almeida, você declara estar de
            acordo com estes termos. Nosso objetivo é oferecer banho, tosa e táxi dog
            com segurança, respeito e profissionalismo.
          </p>

          <h3>Serviços</h3>
          <ul class="terms-list">
            <li>Banho e tosa realizados por profissionais qualificados.</li>
            <li>Cuidados adicionais (hidratação, corte de unhas) conforme avaliação.</li>
            <li>Táxi dog com transporte seguro e adequado ao porte do animal.</li>
          </ul>

          <h3>Agendamentos e Cancelamentos</h3>
          <ul class="terms-list">
            <li>Agendamentos podem ser feitos pelos canais de contato disponíveis.</li>
            <li>Cancelamentos devem ser informados com antecedência mínima de 12 horas.</li>
            <li>Ausências sem aviso podem gerar taxa para compensar o horário reservado.</li>
          </ul>

          <h3>Responsabilidades do Tutor</h3>
          <ul class="terms-list">
            <li>Informar condições de saúde, alergias e histórico comportamental do pet.</li>
            <li>Apresentar carteira de vacinação quando solicitado.</li>
            <li>Uso de coleira/guia adequada e, quando necessário, focinheira para segurança.</li>
          </ul>

          <h3>Saúde e Segurança</h3>
          <ul class="terms-list">
            <li>Podemos recusar o atendimento em casos que representem risco ao pet ou à equipe.</li>
            <li>Pets idosos ou com condições especiais terão manejo adaptado conforme avaliação.</li>
            <li>Qualquer intercorrência será comunicada imediatamente ao tutor.</li>
          </ul>

          <h3>Transporte (Táxi Dog)</h3>
          <ul class="terms-list">
            <li>O transporte é realizado em condições adequadas e com contenção segura.</li>
            <li>Áreas atendidas podem variar conforme disponibilidade e distância.</li>
            <li>Horários são combinados previamente e podem sofrer ajustes por trânsito.</li>
          </ul>

          <h3>Pagamentos e Reembolsos</h3>
          <ul class="terms-list">
            <li>Aceitamos Pix, cartão e dinheiro, conforme indicado na página de pagamento.</li>
            <li>Valores e promoções podem ser atualizados sem aviso prévio.</li>
            <li>Reembolsos são avaliados caso a caso, de acordo com o serviço prestado.</li>
          </ul>

          <h3>Privacidade e Dados</h3>
          <ul class="terms-list">
            <li>Utilizamos seus dados apenas para agendamento e atendimento.</li>
            <li>Informações de contato não são compartilhadas com terceiros sem consentimento.</li>
          </ul>

          <h3>Direitos de Imagem</h3>
          <ul class="terms-list">
            <li>Podemos solicitar autorização para uso de fotos do pet em nossos canais.</li>
            <li>O tutor pode revogar a autorização a qualquer momento pelos canais de contato.</li>
          </ul>

          <h3>Garantias e Limitações</h3>
          <ul class="terms-list">
            <li>Empregamos boas práticas e técnicas reconhecidas nos serviços prestados.</li>
            <li>Resultados estéticos podem variar conforme características individuais do pet.</li>
            <li>Não nos responsabilizamos por informações incorretas fornecidas pelo tutor.</li>
          </ul>

          <h3>Contato</h3>
          <p>
            Dúvidas ou solicitações podem ser feitas pelos canais na seção Contato.
          </p>

          <h3>Atualizações</h3>
          <p>
            Estes termos podem ser atualizados a qualquer momento. O uso contínuo dos
            serviços implica concordância com a versão vigente.
          </p>

          <p class="terms-meta">Última atualização: 12/11/2025</p>
        </div>
      </div>
    </div>

    <FooterBar />
  </div>
  
  
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useHead } from '#imports'
import ContactItem from '~/components/ContactItem.vue'
import ServiceIcon from '~/components/ServiceIcon.vue'
import ThreeDIcon from '~/components/ThreeDIcon.vue'
import ServicesSection from '~/components/ServicesSection.vue'
import CarTaxi3DIcon from '~/components/CarTaxi3DIcon.vue'
import HospitalDog3DIcon from '~/components/HospitalDog3DIcon.vue'
import Bath3DIcon from '~/components/Bath3DIcon.vue'
import Shower3DIcon from '~/components/Shower3DIcon.vue'
import Scissors3DIcon from '~/components/Scissors3DIcon.vue'
import Cat3DIcon from '~/components/Cat3DIcon.vue'
import Dog3DIcon from '~/components/Dog3DIcon.vue'
import Star3DIcon from '~/components/Star3DIcon.vue'
import Razor3DIcon from '~/components/Razor3DIcon.vue'
import Location3DIcon from '~/components/Location3DIcon.vue'
import HeaderBar from '~/components/HeaderBar.vue'
import PixIcon from '~/components/PixIcon.vue'
import CreditCard3DIcon from '~/components/CreditCard3DIcon.vue'
import Dollar3DIcon from '~/components/Dollar3DIcon.vue'

// HeaderBar gerencia o estado de navegação internamente
const navItems = [
  { label: 'Início', href: '#home' },
  { label: 'Sobre', href: '#sobre' },
  { label: 'Serviços', href: '#servicos' },
  { label: 'Pagamento', href: '#pagamento' },
  { label: 'Contato', href: '#contato' }
]
import AgendeAgoraButton from '~/components/AgendeAgoraButton.vue'
import AddressLocationPanel from '~/components/AddressLocationPanel.vue'

useHead({
  htmlAttrs: { lang: 'pt-BR' },
  title: 'Pets Almeida - Cuidado e carinho para seu pet',
  meta: [
    { name: 'description', content: 'Pets Almeida - Banho, tosa e taxi dog em São Paulo. Cuidado e carinho para seu pet.' },
    { name: 'viewport', content: 'width=device-width, initial-scale=1.0' }
  ]
})

const termsOpen = ref(false)

  onMounted(() => {
    // Smooth scroll with offset for sticky header
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
      anchor.addEventListener('click', function (e) {
        const href = anchor.getAttribute('href')
        if (!href) return
        if (href === '#termos') {
          e.preventDefault()
          termsOpen.value = true
          return
        }
        const target = document.querySelector(href)
        if (target) {
          e.preventDefault()
          const header = document.querySelector('header')
          const headerHeight = header?.offsetHeight || 0
          const rect = target.getBoundingClientRect()
          const targetPosition = rect.top + window.pageYOffset - headerHeight
          window.scrollTo({ top: targetPosition, behavior: 'smooth' })
        }
      })
    })

  // Fade-in animation on scroll
  const observerOptions = { threshold: 0.1, rootMargin: '0px 0px -50px 0px' }
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('fade-in')
      }
    })
  }, observerOptions)
  document.querySelectorAll('.service-card, .payment-card, .highlight-item').forEach(el => observer.observe(el))
})
</script>

<style>

@font-face {
  font-family: 'FKGroteskNeue';
  src: url('https://r2cdn.perplexity.ai/fonts/FKGroteskNeue.woff2') format('woff2');
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; font-family: var(--font-family-base); }
body { background-color: var(--color-background); color: var(--color-text); line-height: var(--line-height-normal); overflow-x: hidden; -webkit-font-smoothing: antialiased; text-rendering: optimizeLegibility; }


/* Header */
header { position: sticky; top: 0; background: var(--color-surface); box-shadow: var(--shadow-sm); z-index: 1000; border-bottom: 1px solid var(--color-card-border); }
.header-container { max-width: 1280px; margin: 0 auto; padding: var(--space-16) var(--space-20); display: flex; justify-content: space-between; align-items: center; }
.logo { font-size: var(--font-size-3xl); font-weight: var(--font-weight-bold); color: var(--pet-primary); display: flex; align-items: center; gap: var(--space-8); }
nav ul { display: flex; list-style: none; gap: var(--space-24); }
nav a { color: var(--color-text); text-decoration: none; font-weight: var(--font-weight-medium); transition: color var(--duration-fast) var(--ease-standard); font-size: var(--font-size-base); }
nav a:hover { color: var(--pet-primary); }
.menu-toggle { display: none; background: none; border: none; font-size: 28px; cursor: pointer; color: var(--color-text); }

/* Hero */
  .hero { background: var(--color-bg-8); padding: 80px var(--space-20) 60px; text-align: center; position: relative; isolation: isolate; overflow: hidden; }
  .hero::before { content: ""; position: absolute; inset: 0; background: rgba(0,0,0,0.18); z-index: 0; }
  .hero-content { max-width: 800px; margin: 0 auto; position: relative; z-index: 1; }
.hero h1 { font-size: clamp(32px, 5vw, 48px); color: var(--pet-primary); margin-bottom: var(--space-12); font-weight: var(--font-weight-bold); letter-spacing: var(--letter-spacing-tight); }
.hero .tagline { font-size: var(--font-size-2xl); color: var(--color-text-secondary); margin-bottom: var(--space-32); }
.hero .welcome { font-size: var(--font-size-lg); line-height: 1.6; margin-bottom: var(--space-32); color: var(--color-text); }
.hero-cta { display: flex; flex-direction: column; gap: var(--space-16); align-items: center; }
.cta-button { background: var(--pet-primary); color: white; padding: var(--space-16) var(--space-32); border-radius: var(--radius-lg); text-decoration: none; font-size: var(--font-size-xl); font-weight: var(--font-weight-semibold); box-shadow: var(--shadow-md); transition: all var(--duration-normal) var(--ease-standard); display: inline-block; }
.cta-button:hover { background: #1f4a6b; transform: translateY(-2px); box-shadow: var(--shadow-lg); }
/* .hero-phone removido do hero */

/* Section */
section { padding: 60px var(--space-20); max-width: 1280px; margin: 0 auto; }
section h2 { text-align: center; font-size: var(--font-size-4xl); margin-bottom: var(--space-32); color: var(--pet-primary); font-weight: var(--font-weight-bold); letter-spacing: var(--letter-spacing-tight); }
.about-content { max-width: 800px; margin: 0 auto; text-align: center; }
.about-content p { font-size: var(--font-size-lg); line-height: 1.8; margin-bottom: var(--space-20); color: var(--color-text); }
.highlights { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: var(--space-20); margin-top: var(--space-32); }
.highlight-item { background: var(--color-bg-1); padding: var(--space-20); border-radius: var(--radius-lg); border: 1px solid var(--color-card-border); }
.highlight-item .icon { font-size: 40px; margin-bottom: var(--space-12); }
.highlight-item h3 { font-size: var(--font-size-lg); margin-bottom: var(--space-8); color: var(--color-text); }


/* Payment */
.payment-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: var(--space-20); max-width: 900px; margin: 0 auto; }
.payment-card { background: var(--color-surface); border: 1px solid var(--color-card-border); border-radius: var(--radius-lg); padding: var(--space-24); text-align: center; box-shadow: var(--shadow-sm); transition: all var(--duration-normal) var(--ease-standard); }
.payment-card:hover { transform: translateY(-2px); box-shadow: var(--shadow-md); }
.payment-icon { font-size: 48px; margin-bottom: var(--space-12); }
.payment-method { font-size: var(--font-size-lg); font-weight: var(--font-weight-semibold); margin-bottom: var(--space-8); color: var(--color-text); }
  .payment-note { font-size: var(--font-size-sm); color: var(--color-text-secondary); font-style: italic; }

/* Contact */
#contato { background: var(--color-bg-2); }

/* Modern tweaks */
header { backdrop-filter: saturate(1.1) blur(6px); }
.hero { background: radial-gradient(1000px 500px at 10% -10%, rgba(6,182,212,0.12), transparent 60%), var(--color-bg-8); }
.service-icon { transition: transform var(--duration-normal) var(--ease-standard); }
.service-card:hover .service-icon { transform: translateY(-2px); }
.highlight-item, .service-card, .payment-card { opacity: 0; transform: translateY(8px); will-change: transform, opacity; }
.fade-in { opacity: 1; transform: translateY(0); transition: opacity var(--duration-normal) var(--ease-standard), transform var(--duration-normal) var(--ease-standard); }
.contact-content { max-width: 800px; margin: 0 auto; }
.contact-info { background: var(--color-surface); border: 1px solid var(--color-card-border); border-radius: var(--radius-lg); padding: var(--space-32); margin-bottom: var(--space-32); box-shadow: var(--shadow-sm); }
.contact-item { display: flex; align-items: center; gap: var(--space-16); margin-bottom: var(--space-20); font-size: var(--font-size-lg); }
.contact-item .icon { font-size: 32px; }
.contact-item a { color: var(--pet-primary); text-decoration: none; font-weight: var(--font-weight-medium); }
.contact-item a:hover { text-decoration: underline; }

/* (removido) estilos locais de Serviços Adicionais; agora controlado no ServiceCard */


/* Footer estilizado pelo componente FooterBar */

/* Mobile */
@media (max-width: 768px) {
  /* Navegação móvel encapsulada pelo HeaderBar */
  .services-grid { grid-template-columns: 1fr; }
  .payment-grid { grid-template-columns: 1fr; }
  .highlights { grid-template-columns: 1fr; }
}
@media (max-width: 480px) {
  .hero { padding: 40px var(--space-16); }
  section { padding: 40px var(--space-16); }
  .header-container { padding: var(--space-12) var(--space-16); }
}

/* Animations */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
.fade-in { animation: fadeIn 0.6s var(--ease-standard) forwards; }
</style>

<style>
.terms-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.55); z-index: 10000; display: flex; align-items: center; justify-content: center; padding: var(--space-20); }
.terms-dialog { background: var(--color-surface); color: var(--color-text); border: 1px solid var(--color-card-border); border-radius: var(--radius-lg); box-shadow: var(--shadow-lg); max-width: 1000px; width: 100%; max-height: 85vh; overflow: auto; }
.terms-header { display: flex; align-items: center; justify-content: space-between; padding: var(--space-16) var(--space-20); border-bottom: 1px solid var(--color-card-border); }
.terms-header h2 { font-size: var(--font-size-4xl); color: var(--pet-primary); }
.terms-close { background: transparent; color: var(--color-text); border: 1px solid var(--color-card-border); border-radius: var(--radius-md); padding: 6px 10px; cursor: pointer; font-weight: var(--font-weight-medium); }
.terms-close:hover { background: var(--color-bg-3); }
.terms-content { max-width: 900px; margin: 0 auto; text-align: left; padding: var(--space-20); }
.terms-content h3 { font-size: var(--font-size-xl); margin: var(--space-16) 0 var(--space-8); color: var(--color-text); }
.terms-content p { font-size: var(--font-size-base); line-height: 1.8; color: var(--color-text); margin-bottom: var(--space-12); }
.terms-list { list-style: disc; padding-left: 1.25rem; margin-bottom: var(--space-12); }
.terms-list li { margin-bottom: var(--space-8); color: var(--color-text); font-size: var(--font-size-base); line-height: 1.7; }
.terms-meta { font-size: var(--font-size-sm); color: var(--color-text-secondary); margin-top: var(--space-24); }
</style>
