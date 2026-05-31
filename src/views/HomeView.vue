<template>
  <div class="home">
    <!-- Hero -->
    <section class="hero" aria-label="Sección principal">
      <div class="hero__container">
        <h1 class="hero__title">Impulsamos tu negocio al siguiente nivel</h1>
        <p class="hero__subtitle">
          Somos el Centro de Negocios Santiago de SERCOTEC. Acompañamos a micro, 
          pequeñas y medianas empresas en su crecimiento con asesoría especializada.
        </p>
        <div class="hero__buttons">
          <a href="#servicios" class="btn btn--primary">Ver Servicios</a>
          <router-link to="/contacto" class="btn btn--secondary">Contáctanos</router-link>
        </div>
      </div>
    </section>

    <!-- Servicios -->
    <section id="servicios" class="section" aria-label="Nuestros servicios">
      <div class="section__container">
        <h2 class="section__title">Nuestros Servicios</h2>
        <p class="section__subtitle">Soluciones integrales para tu empresa</p>
        <div class="services__grid" v-if="services.length">
          <ServiceCard
            v-for="service in services"
            :key="service.id"
            :service="service"
          />
        </div>
        <div v-else class="loading">Cargando servicios...</div>
      </div>
    </section>

    <!-- Nosotros -->
    <section id="nosotros" class="section section--gray" aria-label="Sobre nosotros">
      <div class="section__container about">
        <div class="about__text">
          <h2 class="section__title">¿Quiénes somos?</h2>
          <p v-if="about">{{ about.descripcion }}</p>
          <ul class="about__list" v-if="about">
            <li v-for="item in about.puntos" :key="item">✅ {{ item }}</li>
          </ul>
        </div>
        <div class="about__image">
          <img 
            src="https://sitios.sercotec.cl/centros-de-negocios/centro-de-desarrollo-de-negocios-santiago/wp-content/uploads/sites/14/2023/03/Centro-Neg-Stgo.jpg" 
            alt="Centro de Negocios Santiago SERCOTEC"
            loading="lazy"
            width="500"
            height="350"
          />
        </div>
      </div>
    </section>

    <!-- Testimonios -->
    <section id="testimonios" class="section" aria-label="Testimonios de clientes">
      <div class="section__container">
        <h2 class="section__title">Lo que dicen nuestros clientes</h2>
        <TestimonialCarousel :testimonials="testimonials" />
      </div>
    </section>

    <!-- FAQ -->
    <section id="faq" class="section section--gray" aria-label="Preguntas frecuentes">
      <div class="section__container">
        <h2 class="section__title">Preguntas Frecuentes</h2>
        <div class="faq__list" v-if="faqs.length">
          <div 
            class="faq__item" 
            v-for="faq in faqs" 
            :key="faq.id"
          >
            <button 
              class="faq__question"
              @click="toggleFaq(faq.id)"
              :aria-expanded="openFaq === faq.id"
            >
              {{ faq.pregunta }}
              <span>{{ openFaq === faq.id ? '▲' : '▼' }}</span>
            </button>
            <div class="faq__answer" v-show="openFaq === faq.id">
              <p>{{ faq.respuesta }}</p>
            </div>
          </div>
        </div>
        <div v-else class="loading">Cargando preguntas...</div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import ServiceCard from '../components/ServiceCard.vue'
import TestimonialCarousel from '../components/TestimonialCarousel.vue'

export default {
  name: 'HomeView',
  components: { ServiceCard, TestimonialCarousel },
  data() {
    return {
      services: [],
      testimonials: [],
      faqs: [],
      about: null,
      openFaq: null
    }
  },
  async mounted() {
    await this.loadData()
  },
  methods: {
    async loadData() {
      try {
        const [servRes, testRes, faqRes, aboutRes] = await Promise.all([
          axios.get('http://localhost:3001/servicios'),
          axios.get('http://localhost:3001/testimonios'),
          axios.get('http://localhost:3001/faqs'),
          axios.get('http://localhost:3001/nosotros')
        ])
        this.services = servRes.data
        this.testimonials = testRes.data
        this.faqs = faqRes.data
        this.about = aboutRes.data
      } catch (error) {
        console.error('Error cargando datos:', error)
      }
    },
    toggleFaq(id) {
      this.openFaq = this.openFaq === id ? null : id
    }
  }
}
</script>

<style scoped>
.hero {
  background: linear-gradient(135deg, var(--color-primary) 0%, var(--color-accent) 100%);
  color: var(--color-white);
  padding: 5rem 2rem;
  text-align: center;
}

.hero__container {
  max-width: 800px;
  margin: 0 auto;
}

.hero__title {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.hero__subtitle {
  font-size: 1.1rem;
  opacity: 0.9;
  margin-bottom: 2rem;
  line-height: 1.6;
}

.hero__buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  padding: 0.75rem 2rem;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s;
}

.btn--primary {
  background-color: var(--color-secondary);
  color: var(--color-primary);
}

.btn--secondary {
  border: 2px solid var(--color-white);
  color: var(--color-white);
}

.btn--primary:hover { opacity: 0.9; }
.btn--secondary:hover { background-color: rgba(255,255,255,0.1); }

.section {
  padding: 4rem 2rem;
}

.section--gray {
  background-color: var(--color-light);
}

.section__container {
  max-width: 1200px;
  margin: 0 auto;
}

.section__title {
  font-size: 2rem;
  color: var(--color-primary);
  text-align: center;
  margin-bottom: 0.5rem;
}

.section__subtitle {
  text-align: center;
  color: #666;
  margin-bottom: 2.5rem;
}

.services__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.about {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
}

.about__text h2 { text-align: left; }

.about__text p {
  color: #555;
  line-height: 1.7;
  margin-bottom: 1rem;
}

.about__list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.about__list li { color: #444; }

.about__image img {
  width: 100%;
  border-radius: 8px;
  object-fit: cover;
  box-shadow: 0 4px 20px rgba(0,0,0,0.1);
}

.faq__list {
  max-width: 800px;
  margin: 2rem auto 0;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.faq__item {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.faq__question {
  width: 100%;
  padding: 1.25rem;
  background: none;
  border: none;
  text-align: left;
  font-size: 1rem;
  font-weight: 600;
  color: var(--color-primary);
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.faq__answer {
  padding: 0 1.25rem 1.25rem;
  color: #555;
  line-height: 1.6;
}

.loading {
  text-align: center;
  color: #888;
  padding: 2rem;
}

@media (max-width: 768px) {
  .hero__title { font-size: 1.8rem; }
  .about { grid-template-columns: 1fr; }
  .about__image { order: -1; }
}
</style>