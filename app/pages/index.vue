<template>
  <div>
    <header>
      <div class="header-container">
        <div class="logo">🐾 Pets Almeida</div>
        <ThemeToggle />
        <MenuToggle :active="isNavActive" @toggle="isNavActive = !isNavActive" />
        <NavMenu id="mainNav" :items="navItems" :active="isNavActive" @click-link="isNavActive = false" />
      </div>
    </header>

    <section class="hero" id="home">
      <div class="hero-content">
        <h1>🐾 Pets Almeida</h1>
        <p class="tagline">Cuidado e carinho para seu pet</p>
        <p class="welcome">
          Bem-vindo ao Pets Almeida! Somos especializados em banho, tosa e táxi dog em São Paulo.
          Tratamos seu pet com todo amor e profissionalismo que ele merece.
        </p>
        <div class="hero-cta">
          <AgendeAgoraButton />
          <div class="hero-phone">
            📞 <a href="tel:+5511993602794">(11) 99360-2794</a>
          </div>
        </div>
      </div>
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

    <section id="servicos">
      <h2>Nossos Serviços</h2>
      <div class="services-grid">
        <!-- Taxi Dog -->
        <div class="service-card">
          <ServiceIcon aria-label="Táxi Dog">
            <CarTaxi3DIcon />
          </ServiceIcon>
          <h3>Taxi Dog</h3>
          <p class="service-description">Fazemos TAXI DOG</p>
          <div class="service-availability">SOMENTE SÁBADO</div>
          <table class="price-table">
            <thead>
              <tr>
                <th>Distância</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>1 a 2 km</td>
                <td>R$ 10,00</td>
              </tr>
              <tr>
                <td>2 a 4 km</td>
                <td>R$ 20,00</td>
              </tr>
              <tr>
                <td>4 a 6 km</td>
                <td>R$ 40,00</td>
              </tr>
              <tr>
                <td>6 a 10 km</td>
                <td>R$ 60,00</td>
              </tr>
              <tr>
                <td>10 a 15 km</td>
                <td>R$ 80,00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Táxi Pet para Consulta -->
        <div class="service-card">
          <ServiceIcon aria-label="Hospital Pet">
            <HospitalDog3DIcon />
          </ServiceIcon>
          <h3>Táxi Pet para Consulta</h3>
          <p class="service-description">Levamos seu pet para consulta</p>
          <ul class="service-list">
            <li>Hospitais</li>
            <li>Clínicas Veterinárias</li>
            <li>Consultas/Exames</li>
            <li>Castrações</li>
          </ul>
        </div>

        <!-- Banho e Tosa Higiênica -->
        <ServiceCard
          title="Banho e Tosa Higiênica"
          ariaLabel="Banheira"
          :images="['/images/dog.jpg','/images/toby.jpg']"
        >
          <template #icon>
            <Bath3DIcon />
          </template>
          <table class="price-table">
            <thead>
              <tr>
                <th>Porte</th>
                <th>Banho</th>
                <th>Tosa Higiênica</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Mini</td>
                <td>R$ 35,00</td>
                <td>R$ 10,00</td>
              </tr>
              <tr>
                <td>Pequeno</td>
                <td>R$ 45,00</td>
                <td>R$ 20,00</td>
              </tr>
              <tr>
                <td>Médio</td>
                <td>R$ 60,00</td>
                <td>R$ 30,00</td>
              </tr>
              <tr>
                <td>Grande</td>
                <td>R$ 75,00</td>
                <td>R$ 40,00</td>
              </tr>
            </tbody>
          </table>
        </ServiceCard>

        <!-- Somente Banho -->
        <div class="service-card">
          <ServiceIcon aria-label="Ícone de chuveiro">
            <Shower3DIcon />
          </ServiceIcon>
          <h3>Somente Banho</h3>
          <p class="service-description">A partir de:</p>
          <table class="price-table">
            <thead>
              <tr>
                <th>Porte</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Mini</td>
                <td>R$ 35,00</td>
              </tr>
              <tr>
                <td>Pequeno</td>
                <td>R$ 45,00</td>
              </tr>
              <tr>
                <td>Médio</td>
                <td>R$ 60,00</td>
              </tr>
              <tr>
                <td>Grande</td>
                <td>R$ 75,00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Banho Spitz -->
        <div class="service-card">
          <ServiceIcon aria-label="Ícone de estrelas">
            <Star3DIcon />
          </ServiceIcon>
          <h3>Banho Spitz - Lulu da Pomerânia</h3>
          <table class="price-table">
            <thead>
              <tr>
                <th>Porte</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Mini</td>
                <td>R$ 45,00</td>
              </tr>
              <tr>
                <td>Pequeno</td>
                <td>R$ 60,00</td>
              </tr>
              <tr>
                <td>Médio</td>
                <td>R$ 75,00</td>
              </tr>
              <tr>
                <td>Grande</td>
                <td>R$ 85,00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Tosa na Tesoura -->
        <div class="service-card">
          <ServiceIcon aria-label="Ícone de tesoura">
            <Scissors3DIcon />
          </ServiceIcon>
          <h3>Tosa na Tesoura</h3>
          <p class="service-description">A partir de:</p>
          <table class="price-table">
            <thead>
              <tr>
                <th>Porte</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Mini</td>
                <td>R$ 50,00</td>
              </tr>
              <tr>
                <td>Pequeno</td>
                <td>R$ 65,00</td>
              </tr>
              <tr>
                <td>Médio</td>
                <td>R$ 80,00</td>
              </tr>
              <tr>
                <td>Grande</td>
                <td>R$ 95,00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Banho Felinos -->
        <div class="service-card">
          <ServiceIcon aria-label="Ícone de gato/felino">
            <Cat3DIcon />
          </ServiceIcon>
          <h3>Banho Felinos</h3>
          <div class="service-note">INCLUSO CORTE DE UNHA</div>
          <table class="price-table">
            <thead>
              <tr>
                <th>Tipo</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Banho a Seco - Filhote</td>
                <td>R$ 60,00</td>
              </tr>
              <tr>
                <td>Banho a Seco - Adulto</td>
                <td>R$ 100,00</td>
              </tr>
              <tr>
                <td>Banho Molhado - Filhote</td>
                <td>R$ 80,00</td>
              </tr>
              <tr>
                <td>Banho Molhado - Adulto</td>
                <td>R$ 120,00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Tosa Padrão -->
        <div class="service-card">
          <ServiceIcon aria-label="Ícone de cachorro/dog">
            <Dog3DIcon />
          </ServiceIcon>
          <h3>Tosa Padrão</h3>
          <p class="service-description">A partir de:</p>
          <table class="price-table">
            <thead>
              <tr>
                <th>Porte</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Mini</td>
                <td>R$ 40,00</td>
              </tr>
              <tr>
                <td>Pequeno</td>
                <td>R$ 50,00</td>
              </tr>
              <tr>
                <td>Médio</td>
                <td>R$ 60,00</td>
              </tr>
              <tr>
                <td>Grande</td>
                <td>R$ 80,00</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- Tosa Zero -->
        <div class="service-card">
            <ServiceIcon aria-label="Ícone de navalha"><Razor3DIcon /></ServiceIcon>
          <h3>Tosa Zero</h3>
          <p class="service-description">A partir de:</p>
          <table class="price-table">
            <thead>
              <tr>
                <th>Porte</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Mini</td>
                <td>R$ 45,00</td>
              </tr>
              <tr>
                <td>Pequeno</td>
                <td>R$ 55,00</td>
              </tr>
              <tr>
                <td>Médio</td>
                <td>R$ 65,00</td>
              </tr>
              <tr>
                <td>Grande</td>
                <td>R$ 90,00</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <section id="pagamento">
      <h2>Formas de Pagamento</h2>
      <div class="payment-grid">
        <div class="payment-card">
          <div class="payment-icon">💳</div>
          <div class="payment-method">Cartão de Crédito</div>
        </div>
        <div class="payment-card">
          <div class="payment-icon">💳</div>
          <div class="payment-method">Cartão de Débito</div>
          <div class="payment-note">Taxa de maquininha: R$ 5,00</div>
        </div>
        <div class="payment-card">
          <div class="payment-icon"><PixIcon /></div>
          <div class="payment-method">Pix</div>
        </div>
        <div class="payment-card">
          <div class="payment-icon">💵</div>
          <div class="payment-method">Dinheiro</div>
        </div>
      </div>
    </section>

    <section id="contato">
      <h2>Entre em Contato</h2>
      <div class="contact-content">
          <div class="contact-info">
<ContactItem iconName="whatsapp" label="WhatsApp" value="Agendar horário" href="https://wa.me/5511993602794?text=Ol%C3%A1!%20Gostaria%20de%20agendar%20um%20servi%C3%A7o%20para%20meu%20pet." target="_blank" :hideText="false" />
<ContactItem iconName="instagram" label="Instagram" value="@_pets_almeida" href="https://instagram.com/_pets_almeida" target="_blank" :hideText="true" />
          <AddressLocationPanel />
          
        </div>
      </div>
    </section>

    <footer>
      <div class="footer-content">
        <div class="footer-links">
          <a href="#home">Início</a>
          <a href="#sobre">Sobre</a>
          <a href="#servicos">Serviços</a>
          <a href="#pagamento">Pagamento</a>
          <a href="#contato">Contato</a>
        </div>
        <p>&copy; 2025 Pets Almeida - Todos os direitos reservados</p>
        <p class="footer-tagline">Feito com ❤️ para pets</p>
      </div>
    </footer>
  </div>
  
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useHead } from '#imports'
import MenuToggle from '~/components/MenuToggle.vue'
import ContactItem from '~/components/ContactItem.vue'
import NavMenu from '~/components/NavMenu.vue'
import ServiceIcon from '~/components/ServiceIcon.vue'
import ThreeDIcon from '~/components/ThreeDIcon.vue'
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
import ThemeToggle from '~/components/ThemeToggle.vue'
import PixIcon from '~/components/PixIcon.vue'

const isNavActive = ref(false)
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

onMounted(() => {
  // Close menu when clicking on a link
  const navLinks = document.querySelectorAll('nav a')
  navLinks.forEach(link => {
    link.addEventListener('click', () => {
      isNavActive.value = false
    })
  })

  // Smooth scroll with offset for sticky header
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
      const href = anchor.getAttribute('href')
      if (!href) return
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
/* CSS clonado do index (1).html */
:root {
  --color-white: rgba(255, 255, 255, 1);
  --color-black: rgba(0, 0, 0, 1);
  --color-cream-50: rgba(252, 252, 249, 1);
  --color-cream-100: rgba(255, 255, 253, 1);
  --color-gray-200: rgba(245, 245, 245, 1);
  --color-gray-300: rgba(167, 169, 169, 1);
  --color-gray-400: rgba(119, 124, 124, 1);
  --color-slate-500: rgba(98, 108, 113, 1);
  --color-brown-600: rgba(94, 82, 64, 1);
  --color-charcoal-700: rgba(31, 33, 33, 1);
  --color-charcoal-800: rgba(38, 40, 40, 1);
  --color-slate-900: rgba(19, 52, 59, 1);
  --color-teal-300: rgba(50, 184, 198, 1);
  --color-teal-400: rgba(45, 166, 178, 1);
  --color-teal-500: rgba(33, 128, 141, 1);
  --color-teal-600: rgba(29, 116, 128, 1);
  --color-teal-700: rgba(26, 104, 115, 1);
  --color-teal-800: rgba(41, 150, 161, 1);
  --color-red-400: rgba(255, 84, 89, 1);
  --color-red-500: rgba(192, 21, 47, 1);
  --color-orange-400: rgba(230, 129, 97, 1);
  --color-orange-500: rgba(168, 75, 47, 1);
  --color-brown-600-rgb: 94, 82, 64;
  --color-teal-500-rgb: 33, 128, 141;
  --color-slate-900-rgb: 19, 52, 59;
  --color-slate-500-rgb: 98, 108, 113;
  --color-red-500-rgb: 192, 21, 47;
  --color-red-400-rgb: 255, 84, 89;
  --color-orange-500-rgb: 168, 75, 47;
  --color-orange-400-rgb: 230, 129, 97;
  --color-bg-1: rgba(59, 130, 246, 0.08);
  --color-bg-2: rgba(245, 158, 11, 0.08);
  --color-bg-3: rgba(34, 197, 94, 0.08);
  --color-bg-4: rgba(239, 68, 68, 0.08);
  --color-bg-5: rgba(147, 51, 234, 0.08);
  --color-bg-6: rgba(249, 115, 22, 0.08);
  --color-bg-7: rgba(236, 72, 153, 0.08);
  --color-bg-8: rgba(6, 182, 212, 0.08);
  --color-background: var(--color-cream-50);
  --color-surface: var(--color-cream-100);
  --color-text: var(--color-slate-900);
  --color-text-secondary: var(--color-slate-500);
  --color-primary: var(--color-teal-500);
  --color-primary-hover: var(--color-teal-600);
  --color-primary-active: var(--color-teal-700);
  --color-secondary: rgba(var(--color-brown-600-rgb), 0.12);
  --color-secondary-hover: rgba(var(--color-brown-600-rgb), 0.2);
  --color-secondary-active: rgba(var(--color-brown-600-rgb), 0.25);
  --color-border: rgba(var(--color-brown-600-rgb), 0.2);
  --color-btn-primary-text: var(--color-cream-50);
  --color-card-border: rgba(var(--color-brown-600-rgb), 0.12);
  --color-card-border-inner: rgba(var(--color-brown-600-rgb), 0.12);
  --color-error: var(--color-red-500);
  --color-success: var(--color-teal-500);
  --color-warning: var(--color-orange-500);
  --color-info: var(--color-slate-500);
  --color-focus-ring: rgba(var(--color-teal-500-rgb), 0.4);
  --color-select-caret: rgba(var(--color-slate-900-rgb), 0.8);
  --focus-ring: 0 0 0 3px var(--color-focus-ring);
  --focus-outline: 2px solid var(--color-primary);
  --status-bg-opacity: 0.15;
  --status-border-opacity: 0.25;
  --select-caret-light: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%23134252' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  --select-caret-dark: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='16' height='16' viewBox='0 0 24 24' fill='none' stroke='%23f5f5f5' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  --color-success-rgb: 33, 128, 141;
  --color-error-rgb: 192, 21, 47;
  --color-warning-rgb: 168, 75, 47;
  --color-info-rgb: 98, 108, 113;
  --font-family-base: "FKGroteskNeue", "Geist", "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  --font-family-mono: "Berkeley Mono", ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
  --font-size-xs: 11px;
  --font-size-sm: 12px;
  --font-size-base: 14px;
  --font-size-md: 14px;
  --font-size-lg: 16px;
  --font-size-xl: 18px;
  --font-size-2xl: 20px;
  --font-size-3xl: 24px;
  --font-size-4xl: 30px;
  --font-weight-normal: 400;
  --font-weight-medium: 500;
  --font-weight-semibold: 550;
  --font-weight-bold: 600;
  --line-height-tight: 1.2;
  --line-height-normal: 1.5;
  --letter-spacing-tight: -0.01em;
  --space-0: 0;
  --space-1: 1px;
  --space-2: 2px;
  --space-4: 4px;
  --space-6: 6px;
  --space-8: 8px;
  --space-10: 10px;
  --space-12: 12px;
  --space-16: 16px;
  --space-20: 20px;
  --space-24: 24px;
  --space-32: 32px;
  --radius-sm: 6px;
  --radius-base: 8px;
  --radius-md: 10px;
  --radius-lg: 12px;
  --radius-full: 9999px;
  --shadow-xs: 0 1px 2px rgba(0, 0, 0, 0.02);
  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.04), 0 1px 2px rgba(0, 0, 0, 0.02);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.04), 0 2px 4px -1px rgba(0, 0, 0, 0.02);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.04), 0 4px 6px -2px rgba(0, 0, 0, 0.02);
  --shadow-inset-sm: inset 0 1px 0 rgba(255, 255, 255, 0.15), inset 0 -1px 0 rgba(0, 0, 0, 0.03);
  --duration-fast: 150ms;
  --duration-normal: 250ms;
  --ease-standard: cubic-bezier(0.16, 1, 0.3, 1);
  --container-sm: 640px;
  --container-md: 768px;
  --container-lg: 1024px;
  --container-xl: 1280px;

  --pet-primary: #2B5F8D;
  --pet-secondary: #87CEEB;
  --pet-accent: #FFD700;
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-gray-400-rgb: 119, 124, 124;
    --color-teal-300-rgb: 50, 184, 198;
    --color-gray-300-rgb: 167, 169, 169;
    --color-gray-200-rgb: 245, 245, 245;
    --color-bg-1: rgba(29, 78, 216, 0.15);
    --color-bg-2: rgba(180, 83, 9, 0.15);
    --color-bg-3: rgba(21, 128, 61, 0.15);
    --color-bg-4: rgba(185, 28, 28, 0.15);
    --color-bg-5: rgba(107, 33, 168, 0.15);
    --color-bg-6: rgba(194, 65, 12, 0.15);
    --color-bg-7: rgba(190, 24, 93, 0.15);
    --color-bg-8: rgba(8, 145, 178, 0.15);
    --color-background: var(--color-charcoal-700);
    --color-surface: var(--color-charcoal-800);
    --color-text: var(--color-gray-200);
    --color-text-secondary: rgba(var(--color-gray-300-rgb), 0.7);
    --color-primary: var(--color-teal-300);
    --color-primary-hover: var(--color-teal-400);
    --color-primary-active: var(--color-teal-800);
    --color-secondary: rgba(var(--color-gray-400-rgb), 0.15);
    --color-secondary-hover: rgba(var(--color-gray-400-rgb), 0.25);
    --color-secondary-active: rgba(var(--color-gray-400-rgb), 0.3);
    --color-border: rgba(var(--color-gray-400-rgb), 0.3);
    --color-error: var(--color-red-400);
    --color-success: var(--color-teal-300);
    --color-warning: var(--color-orange-400);
    --color-info: var(--color-gray-300);
    --color-focus-ring: rgba(var(--color-teal-300-rgb), 0.4);
    --color-btn-primary-text: var(--color-slate-900);
    --color-card-border: rgba(var(--color-gray-400-rgb), 0.2);
    --color-card-border-inner: rgba(var(--color-gray-400-rgb), 0.15);
    --shadow-inset-sm: inset 0 1px 0 rgba(255, 255, 255, 0.1), inset 0 -1px 0 rgba(0, 0, 0, 0.15);
    --color-border-secondary: rgba(var(--color-gray-400-rgb), 0.2);
    --color-select-caret: rgba(var(--color-gray-200-rgb), 0.8);
    --color-success-rgb: var(--color-teal-300-rgb);
    --color-error-rgb: var(--color-red-400-rgb);
    --color-warning-rgb: var(--color-orange-400-rgb);
    --color-info-rgb: var(--color-gray-300-rgb);
  }
}

@font-face {
  font-family: 'FKGroteskNeue';
  src: url('https://r2cdn.perplexity.ai/fonts/FKGroteskNeue.woff2') format('woff2');
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; font-family: var(--font-family-base); }
body { background-color: var(--color-background); color: var(--color-text); line-height: var(--line-height-normal); overflow-x: hidden; }

/* Tema Black explícito */
html.theme-black {
  --color-background: #0b0c0d;
  --color-surface: #101214;
  --color-text: #f5f7fa;
  --color-text-secondary: rgba(245, 247, 250, 0.72);
  --color-primary: var(--pet-primary);
  --color-primary-hover: #1f4a6b;
  --color-primary-active: #183a53;
  --color-secondary: rgba(255,255,255,0.06);
  --color-secondary-hover: rgba(255,255,255,0.1);
  --color-secondary-active: rgba(255,255,255,0.12);
  --color-border: rgba(255,255,255,0.08);
  --color-card-border: rgba(255,255,255,0.08);
  --color-card-border-inner: rgba(255,255,255,0.06);
  --color-error: var(--color-red-400);
  --color-success: var(--color-teal-300);
  --color-warning: var(--color-orange-400);
  --color-info: var(--color-gray-300);
  --color-focus-ring: rgba(43, 95, 141, 0.4);
  --color-select-caret: rgba(245,245,245,0.8);
  --color-bg-1: rgba(59, 130, 246, 0.08);
  --color-bg-2: rgba(245, 158, 11, 0.08);
  --color-bg-3: rgba(34, 197, 94, 0.08);
  --color-bg-4: rgba(239, 68, 68, 0.08);
  --color-bg-5: rgba(147, 51, 234, 0.08);
  --color-bg-6: rgba(249, 115, 22, 0.08);
  --color-bg-7: rgba(236, 72, 153, 0.08);
  --color-bg-8: rgba(6, 182, 212, 0.08);
}

/* Header */
header { position: sticky; top: 0; background: var(--color-surface); box-shadow: var(--shadow-sm); z-index: 1000; border-bottom: 1px solid var(--color-card-border); }
.header-container { max-width: 1280px; margin: 0 auto; padding: var(--space-16) var(--space-20); display: flex; justify-content: space-between; align-items: center; }
.logo { font-size: var(--font-size-3xl); font-weight: var(--font-weight-bold); color: var(--pet-primary); display: flex; align-items: center; gap: var(--space-8); }
nav ul { display: flex; list-style: none; gap: var(--space-24); }
nav a { color: var(--color-text); text-decoration: none; font-weight: var(--font-weight-medium); transition: color var(--duration-fast) var(--ease-standard); font-size: var(--font-size-base); }
nav a:hover { color: var(--pet-primary); }
.menu-toggle { display: none; background: none; border: none; font-size: 28px; cursor: pointer; color: var(--color-text); }

/* Hero */
.hero { background: var(--color-bg-8); padding: 80px var(--space-20) 60px; text-align: center; }
.hero-content { max-width: 800px; margin: 0 auto; }
.hero h1 { font-size: clamp(32px, 5vw, 48px); color: var(--pet-primary); margin-bottom: var(--space-12); font-weight: var(--font-weight-bold); }
.hero .tagline { font-size: var(--font-size-2xl); color: var(--color-text-secondary); margin-bottom: var(--space-32); }
.hero .welcome { font-size: var(--font-size-lg); line-height: 1.6; margin-bottom: var(--space-32); color: var(--color-text); }
.hero-cta { display: flex; flex-direction: column; gap: var(--space-16); align-items: center; }
.cta-button { background: var(--pet-primary); color: white; padding: var(--space-16) var(--space-32); border-radius: var(--radius-lg); text-decoration: none; font-size: var(--font-size-xl); font-weight: var(--font-weight-semibold); box-shadow: var(--shadow-md); transition: all var(--duration-normal) var(--ease-standard); display: inline-block; }
.cta-button:hover { background: #1f4a6b; transform: translateY(-2px); box-shadow: var(--shadow-lg); }
.hero-phone { font-size: var(--font-size-2xl); font-weight: var(--font-weight-bold); color: var(--pet-primary); }
.hero-phone a { color: var(--pet-primary); text-decoration: none; }

/* Section */
section { padding: 60px var(--space-20); max-width: 1280px; margin: 0 auto; }
section h2 { text-align: center; font-size: var(--font-size-4xl); margin-bottom: var(--space-32); color: var(--pet-primary); font-weight: var(--font-weight-bold); }
.about-content { max-width: 800px; margin: 0 auto; text-align: center; }
.about-content p { font-size: var(--font-size-lg); line-height: 1.8; margin-bottom: var(--space-20); color: var(--color-text); }
.highlights { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: var(--space-20); margin-top: var(--space-32); }
.highlight-item { background: var(--color-bg-1); padding: var(--space-20); border-radius: var(--radius-lg); border: 1px solid var(--color-card-border); }
.highlight-item .icon { font-size: 40px; margin-bottom: var(--space-12); }
.highlight-item h3 { font-size: var(--font-size-lg); margin-bottom: var(--space-8); color: var(--color-text); }

/* Services */
.services-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: var(--space-24); }
.service-card { background: var(--color-surface); border: 1px solid var(--color-card-border); border-radius: var(--radius-lg); padding: var(--space-24); box-shadow: var(--shadow-sm); transition: all var(--duration-normal) var(--ease-standard); }
.service-card:hover { transform: translateY(-4px); box-shadow: var(--shadow-lg); border-color: var(--pet-secondary); }
.service-icon { font-size: 48px; margin-bottom: var(--space-16); }
.service-icon img { width: 1em; height: 1em; display: inline-block; }
.service-icon svg { width: 1em; height: 1em; display: inline-block; }
.service-card h3 { font-size: var(--font-size-xl); margin-bottom: var(--space-12); color: var(--pet-primary); font-weight: var(--font-weight-semibold); }
.service-description { color: var(--color-text-secondary); margin-bottom: var(--space-16); font-size: var(--font-size-base); }
.service-availability { background: var(--pet-accent); color: var(--color-slate-900); padding: var(--space-6) var(--space-12); border-radius: var(--radius-base); font-size: var(--font-size-sm); font-weight: var(--font-weight-semibold); display: inline-block; margin-bottom: var(--space-16); }
.service-note { background: var(--color-bg-3); color: var(--color-text); padding: var(--space-8) var(--space-12); border-radius: var(--radius-base); font-size: var(--font-size-sm); font-weight: var(--font-weight-medium); margin-bottom: var(--space-16); border: 1px solid var(--color-card-border); }
.price-table { width: 100%; border-collapse: collapse; margin-top: var(--space-12); }
.price-table th, .price-table td { padding: var(--space-10) var(--space-12); text-align: left; border-bottom: 1px solid var(--color-card-border); font-size: var(--font-size-base); }
.price-table th { background: var(--color-bg-1); font-weight: var(--font-weight-semibold); color: var(--color-text); }
.price-table td:last-child { font-weight: var(--font-weight-semibold); color: var(--pet-primary); }
.service-list { list-style: none; margin-top: var(--space-12); }
.service-list li { padding: var(--space-8) 0; padding-left: var(--space-24); position: relative; font-size: var(--font-size-base); }
.service-list li::before { content: '✓'; position: absolute; left: 0; color: var(--pet-primary); font-weight: var(--font-weight-bold); }

/* Payment */
.payment-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: var(--space-20); max-width: 900px; margin: 0 auto; }
.payment-card { background: var(--color-surface); border: 1px solid var(--color-card-border); border-radius: var(--radius-lg); padding: var(--space-24); text-align: center; box-shadow: var(--shadow-sm); transition: all var(--duration-normal) var(--ease-standard); }
.payment-card:hover { transform: translateY(-2px); box-shadow: var(--shadow-md); }
.payment-icon { font-size: 48px; margin-bottom: var(--space-12); }
.payment-method { font-size: var(--font-size-lg); font-weight: var(--font-weight-semibold); margin-bottom: var(--space-8); color: var(--color-text); }
.payment-note { font-size: var(--font-size-sm); color: var(--color-text-secondary); font-style: italic; }

/* Contact */
#contato { background: var(--color-bg-2); }
.contact-content { max-width: 800px; margin: 0 auto; }
.contact-info { background: var(--color-surface); border: 1px solid var(--color-card-border); border-radius: var(--radius-lg); padding: var(--space-32); margin-bottom: var(--space-32); box-shadow: var(--shadow-sm); }
.contact-item { display: flex; align-items: center; gap: var(--space-16); margin-bottom: var(--space-20); font-size: var(--font-size-lg); }
.contact-item .icon { font-size: 32px; }
.contact-item a { color: var(--pet-primary); text-decoration: none; font-weight: var(--font-weight-medium); }
.contact-item a:hover { text-decoration: underline; }


/* Footer */
footer { background: var(--color-surface); border-top: 1px solid var(--color-card-border); padding: var(--space-32) var(--space-20); text-align: center; }
.footer-content { max-width: 1280px; margin: 0 auto; }
.footer-links { display: flex; justify-content: center; gap: var(--space-32); margin-bottom: var(--space-20); flex-wrap: wrap; }
.footer-links a { color: var(--color-text); text-decoration: none; font-size: var(--font-size-base); }
.footer-links a:hover { color: var(--pet-primary); }
.footer-tagline { color: var(--color-text-secondary); margin-top: var(--space-16); font-size: var(--font-size-base); }

/* Mobile */
@media (max-width: 768px) {
  .menu-toggle { display: block; }
  nav { position: fixed; top: 70px; left: -100%; width: 100%; background: var(--color-surface); padding: var(--space-24); box-shadow: var(--shadow-lg); transition: left var(--duration-normal) var(--ease-standard); border-bottom: 1px solid var(--color-card-border); }
  nav.active { left: 0; }
  nav ul { flex-direction: column; gap: var(--space-16); }
  nav a { font-size: var(--font-size-lg); display: block; padding: var(--space-12); }
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
