<template>
  <footer class="footer" role="contentinfo">
    <div class="footer__container">
      <div class="footer__info">
        <h3 class="footer__title">Centro de Negocios Santiago</h3>
        <p class="footer__subtitle">SERCOTEC</p>
        <p class="footer__address">
          📍 Manuel Rodríguez Sur 749, Santiago (Metro Toesca)
        </p>
        <a href="mailto:centro.santiago@centrossercotec.cl" class="footer__email">
          ✉️ centro.santiago@centrossercotec.cl
        </a>
      </div>

      <div class="footer__links">
        <h4>Navegación</h4>
        <ul>
          <li><a href="/#servicios">Servicios</a></li>
          <li><a href="/#nosotros">Nosotros</a></li>
          <li><a href="/#testimonios">Testimonios</a></li>
          <li><a href="/#faq">Preguntas Frecuentes</a></li>
          <li><router-link to="/contacto">Contacto</router-link></li>
        </ul>
      </div>

      <div class="footer__social">
        <h4>Síguenos</h4>
        <a 
          href="https://www.facebook.com/centrodnsantiago" 
          target="_blank"
          rel="noopener noreferrer"
          aria-label="Facebook de Centro de Negocios Santiago"
        >
          Facebook
        </a>
      </div>
    </div>

    <div class="footer__bottom">
      <p>© {{ currentYear }} Centro de Negocios Santiago · SERCOTEC. Todos los derechos reservados.</p>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'AppFooter',
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
}
</script>

<style scoped>
.footer {
  background-color: var(--color-primary);
  color: var(--color-white);
  padding: 3rem 2rem 1rem;
  margin-top: auto;
}

.footer__container {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  padding-bottom: 2rem;
  border-bottom: 1px solid rgba(255,255,255,0.2);
}

.footer__title {
  font-size: 1.1rem;
  margin-bottom: 0.25rem;
}

.footer__subtitle {
  color: var(--color-secondary);
  font-weight: 600;
  margin-bottom: 1rem;
}

.footer__address {
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  opacity: 0.85;
}

.footer__email {
  color: var(--color-secondary);
  text-decoration: none;
  font-size: 0.9rem;
}

.footer__links h4,
.footer__social h4 {
  color: var(--color-secondary);
  margin-bottom: 1rem;
}

.footer__links ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.footer__links a,
.footer__social a {
  color: var(--color-white);
  text-decoration: none;
  font-size: 0.9rem;
  opacity: 0.85;
  transition: opacity 0.3s;
}

.footer__links a:hover,
.footer__social a:hover {
  opacity: 1;
  color: var(--color-secondary);
}

.footer__bottom {
  max-width: 1200px;
  margin: 1rem auto 0;
  text-align: center;
  font-size: 0.8rem;
  opacity: 0.7;
}

@media (max-width: 768px) {
  .footer__container {
    grid-template-columns: 1fr;
  }
}
</style>