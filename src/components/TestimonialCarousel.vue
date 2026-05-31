<template>
  <div class="carousel" role="region" aria-label="Carrusel de testimonios">
    <div class="carousel__track" :style="trackStyle">
      <div 
        class="carousel__slide"
        v-for="(testimonial, index) in testimonials"
        :key="testimonial.id"
        :aria-hidden="index !== currentIndex"
      >
        <div class="carousel__card">
          <div class="carousel__quote">"</div>
          <p class="carousel__text">{{ testimonial.comentario }}</p>
          <div class="carousel__author">
            <img 
              :src="testimonial.avatar" 
              :alt="'Foto de ' + testimonial.nombre"
              class="carousel__avatar"
              loading="lazy"
              width="50"
              height="50"
            />
            <div>
              <p class="carousel__name">{{ testimonial.nombre }}</p>
              <p class="carousel__company">{{ testimonial.empresa }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Controles -->
    <div class="carousel__controls">
      <button 
        class="carousel__btn"
        @click="prev"
        aria-label="Testimonio anterior"
        :disabled="testimonials.length <= 1"
      >
        &#8592;
      </button>

      <div class="carousel__dots" role="tablist">
        <button
          v-for="(_, index) in testimonials"
          :key="index"
          class="carousel__dot"
          :class="{ 'carousel__dot--active': index === currentIndex }"
          @click="goTo(index)"
          :aria-label="'Ir al testimonio ' + (index + 1)"
          :aria-selected="index === currentIndex"
          role="tab"
        ></button>
      </div>

      <button 
        class="carousel__btn"
        @click="next"
        aria-label="Testimonio siguiente"
        :disabled="testimonials.length <= 1"
      >
        &#8594;
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TestimonialCarousel',
  props: {
    testimonials: {
      type: Array,
      required: true,
      default: () => []
    }
  },
  data() {
    return {
      currentIndex: 0,
      autoPlayInterval: null
    }
  },
  computed: {
    trackStyle() {
      return {
        transform: `translateX(-${this.currentIndex * 100}%)`
      }
    }
  },
  mounted() {
    this.startAutoPlay()
  },
  beforeUnmount() {
    this.stopAutoPlay()
  },
  methods: {
    next() {
      this.currentIndex = (this.currentIndex + 1) % this.testimonials.length
    },
    prev() {
      this.currentIndex = (this.currentIndex - 1 + this.testimonials.length) % this.testimonials.length
    },
    goTo(index) {
      this.currentIndex = index
    },
    startAutoPlay() {
      this.autoPlayInterval = setInterval(this.next, 5000)
    },
    stopAutoPlay() {
      clearInterval(this.autoPlayInterval)
    }
  }
}
</script>

<style scoped>
.carousel {
  position: relative;
  overflow: hidden;
  max-width: 800px;
  margin: 2rem auto 0;
}

.carousel__track {
  display: flex;
  transition: transform 0.5s ease;
}

.carousel__slide {
  min-width: 100%;
  padding: 0 1rem;
}

.carousel__card {
  background: var(--color-white);
  border-radius: 12px;
  padding: 2rem;
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
  position: relative;
}

.carousel__quote {
  font-size: 4rem;
  color: var(--color-secondary);
  line-height: 1;
  margin-bottom: 0.5rem;
  font-family: Georgia, serif;
}

.carousel__text {
  color: #444;
  font-size: 1.05rem;
  line-height: 1.7;
  margin-bottom: 1.5rem;
  font-style: italic;
}

.carousel__author {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.carousel__avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--color-secondary);
}

.carousel__name {
  font-weight: 700;
  color: var(--color-primary);
}

.carousel__company {
  font-size: 0.85rem;
  color: #888;
}

.carousel__controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  margin-top: 1.5rem;
}

.carousel__btn {
  background-color: var(--color-primary);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 1.2rem;
  cursor: pointer;
  transition: background-color 0.3s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel__btn:hover:not(:disabled) {
  background-color: var(--color-accent);
}

.carousel__btn:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}

.carousel__dots {
  display: flex;
  gap: 0.5rem;
}

.carousel__dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: none;
  background-color: #ccc;
  cursor: pointer;
  transition: background-color 0.3s;
  padding: 0;
}

.carousel__dot--active {
  background-color: var(--color-primary);
}

@media (max-width: 768px) {
  .carousel__card {
    padding: 1.5rem;
  }

  .carousel__text {
    font-size: 0.95rem;
  }
}
</style>