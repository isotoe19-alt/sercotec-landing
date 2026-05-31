<template>
  <article class="card" role="article">
    <div class="card__image-wrapper">
      <img 
        :src="service.imagen" 
        :alt="'Imagen del servicio: ' + service.titulo"
        class="card__image"
        loading="lazy"
        width="300"
        height="200"
      />
    </div>
    <div class="card__body">
      <h3 class="card__title">{{ service.titulo }}</h3>
      <p class="card__description">{{ service.descripcion }}</p>
      <router-link 
        :to="{ path: '/contacto', query: { servicio: service.titulo }}"
        class="card__btn"
        :aria-label="'Contáctanos sobre ' + service.titulo"
      >
        Contáctanos
      </router-link>
    </div>
  </article>
</template>

<script>
export default {
  name: 'ServiceCard',
  props: {
    service: {
      type: Object,
      required: true,
      validator(value) {
        return value.id && value.titulo && value.descripcion
      }
    }
  }
}
</script>

<style scoped>
.card {
  background: var(--color-white);
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 12px rgba(0,0,0,0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  display: flex;
  flex-direction: column;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
}

.card__image-wrapper {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.card__image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s;
}

.card:hover .card__image {
  transform: scale(1.05);
}

.card__body {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  flex: 1;
  gap: 0.75rem;
}

.card__title {
  font-size: 1.1rem;
  color: var(--color-primary);
  font-weight: 700;
}

.card__description {
  color: #555;
  font-size: 0.95rem;
  line-height: 1.6;
  flex: 1;
}

.card__btn {
  display: inline-block;
  background-color: var(--color-primary);
  color: var(--color-white);
  padding: 0.6rem 1.5rem;
  border-radius: 4px;
  text-decoration: none;
  font-weight: 600;
  text-align: center;
  transition: background-color 0.3s;
  align-self: flex-start;
}

.card__btn:hover {
  background-color: var(--color-accent);
}
</style>