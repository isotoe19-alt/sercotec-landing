<template>
  <nav class="navbar" role="navigation" aria-label="Navegación principal">
    <div class="navbar__container">
      <a href="/" class="navbar__logo">
        <span class="navbar__logo-text">Centro de Negocios</span>
        <span class="navbar__logo-sub">Santiago · SERCOTEC</span>
      </a>
      <button class="navbar__toggle" @click="toggleMenu" :aria-expanded="menuOpen" aria-controls="nav-menu" aria-label="Abrir menú">
        <span></span><span></span><span></span>
      </button>
      <ul class="navbar__menu" :class="{ 'navbar__menu--open': menuOpen }" id="nav-menu">
        <li><router-link to="/" @click="closeMenu">Inicio</router-link></li>
        <li><a href="/#servicios" @click="closeMenu">Servicios</a></li>
        <li><a href="/#nosotros" @click="closeMenu">Nosotros</a></li>
        <li><a href="/#testimonios" @click="closeMenu">Testimonios</a></li>
        <li><a href="/#faq" @click="closeMenu">FAQ</a></li>
        <li><router-link to="/contacto" class="navbar__cta" @click="closeMenu">Contáctanos</router-link></li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return { menuOpen: false }
  },
  methods: {
    toggleMenu() { this.menuOpen = !this.menuOpen },
    closeMenu() { this.menuOpen = false }
  }
}
</script>

<style scoped>
.navbar {
  background-color: var(--color-primary);
  padding: 1rem 2rem;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}
.navbar__container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.navbar__logo { text-decoration: none; display: flex; flex-direction: column; }
.navbar__logo-text { color: var(--color-white); font-size: 1.1rem; font-weight: 700; }
.navbar__logo-sub { color: var(--color-secondary); font-size: 0.75rem; }
.navbar__menu { list-style: none; display: flex; gap: 1.5rem; align-items: center; }
.navbar__menu a { color: var(--color-white); text-decoration: none; font-size: 0.95rem; transition: color 0.3s; }
.navbar__menu a:hover { color: var(--color-secondary); }
.navbar__cta { background-color: var(--color-secondary); color: var(--color-primary) !important; padding: 0.5rem 1.2rem; border-radius: 4px; font-weight: 600; }
.navbar__toggle { display: none; flex-direction: column; gap: 5px; background: none; border: none; cursor: pointer; padding: 4px; }
.navbar__toggle span { display: block; width: 25px; height: 3px; background-color: var(--color-white); border-radius: 3px; }
@media (max-width: 768px) {
  .navbar__toggle { display: flex; }
  .navbar__menu { display: none; flex-direction: column; position: absolute; top: 70px; left: 0; right: 0; background-color: var(--color-primary); padding: 1rem 2rem; gap: 1rem; }
  .navbar__menu--open { display: flex; }
}
</style>