<template>
  <div class="contact">
    <div class="contact__header">
      <h1>Contáctanos</h1>
      <p>Estamos aquí para ayudarte a hacer crecer tu negocio</p>
    </div>

    <div class="contact__container">
      <!-- Formulario -->
      <div class="contact__form-wrapper">
        <form 
          class="contact__form"
          @submit.prevent="handleSubmit"
          novalidate
          aria-label="Formulario de contacto"
        >
          <div class="form__group">
            <label for="nombre">Nombre completo *</label>
            <input 
              id="nombre"
              v-model="form.nombre"
              type="text"
              placeholder="Tu nombre"
              :class="{ 'input--error': errors.nombre }"
              aria-required="true"
              :aria-describedby="errors.nombre ? 'error-nombre' : null"
            />
            <span v-if="errors.nombre" id="error-nombre" class="form__error" role="alert">
              {{ errors.nombre }}
            </span>
          </div>

          <div class="form__group">
            <label for="email">Correo electrónico *</label>
            <input 
              id="email"
              v-model="form.email"
              type="email"
              placeholder="tucorreo@ejemplo.cl"
              :class="{ 'input--error': errors.email }"
              aria-required="true"
              :aria-describedby="errors.email ? 'error-email' : null"
            />
            <span v-if="errors.email" id="error-email" class="form__error" role="alert">
              {{ errors.email }}
            </span>
          </div>

          <div class="form__group">
            <label for="telefono">Teléfono</label>
            <input 
              id="telefono"
              v-model="form.telefono"
              type="tel"
              placeholder="+56 9 1234 5678"
            />
          </div>

          <div class="form__group">
            <label for="servicio">Servicio de interés *</label>
            <select 
              id="servicio"
              v-model="form.servicio"
              :class="{ 'input--error': errors.servicio }"
              aria-required="true"
            >
              <option value="">Selecciona un servicio</option>
              <option v-for="s in servicios" :key="s.id" :value="s.titulo">
                {{ s.titulo }}
              </option>
            </select>
            <span v-if="errors.servicio" class="form__error" role="alert">
              {{ errors.servicio }}
            </span>
          </div>

          <div class="form__group">
            <label for="mensaje">Mensaje *</label>
            <textarea 
              id="mensaje"
              v-model="form.mensaje"
              rows="5"
              placeholder="Cuéntanos sobre tu negocio y cómo podemos ayudarte..."
              :class="{ 'input--error': errors.mensaje }"
              aria-required="true"
              :aria-describedby="errors.mensaje ? 'error-mensaje' : null"
            ></textarea>
            <span v-if="errors.mensaje" id="error-mensaje" class="form__error" role="alert">
              {{ errors.mensaje }}
            </span>
          </div>

          <!-- Honeypot anti-bots -->
          <div class="form__honeypot" aria-hidden="true">
            <label for="website">No llenar este campo</label>
            <input id="website" v-model="form.honeypot" type="text" tabindex="-1" autocomplete="off" />
          </div>

          <button 
            type="submit" 
            class="form__submit"
            :disabled="isSubmitting"
            aria-busy="isSubmitting"
          >
            {{ isSubmitting ? 'Enviando...' : 'Enviar mensaje' }}
          </button>

          <!-- Mensaje de éxito -->
          <div v-if="submitSuccess" class="form__success" role="alert">
            ✅ ¡Mensaje enviado! Nos contactaremos contigo pronto.
          </div>
        </form>
      </div>

      <!-- Info de contacto -->
      <div class="contact__info">
        <h2>Información de contacto</h2>

        <div class="info__item">
          <span class="info__icon">📍</span>
          <div>
            <strong>Dirección</strong>
            <p>Manuel Rodríguez Sur 749, Santiago</p>
            <p>Metro Toesca</p>
          </div>
        </div>

        <div class="info__item">
          <span class="info__icon">✉️</span>
          <div>
            <strong>Correo</strong>
            <a href="mailto:centro.santiago@centrossercotec.cl">
              centro.santiago@centrossercotec.cl
            </a>
          </div>
        </div>

        <div class="info__item">
          <span class="info__icon">🕐</span>
          <div>
            <strong>Horario</strong>
            <p>Lunes a Viernes: 9:00 - 18:00</p>
          </div>
        </div>

        <div class="contact__map">
          <iframe
            title="Ubicación Centro de Negocios Santiago"
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3329.5!2d-70.6506!3d-33.4569!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zManuel+Rodr%C3%ADguez+Sur+749!5e0!3m2!1ses!2scl!4v1"
            width="100%"
            height="200"
            style="border:0; border-radius: 8px;"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ContactView',
  data() {
    return {
      form: {
        nombre: '',
        email: '',
        telefono: '',
        servicio: '',
        mensaje: '',
        honeypot: ''
      },
      errors: {},
      isSubmitting: false,
      submitSuccess: false,
      servicios: []
    }
  },
  async mounted() {
    // Prellenar servicio desde query param
    if (this.$route.query.servicio) {
      this.form.servicio = this.$route.query.servicio
    }
    await this.loadServicios()
  },
  methods: {
    async loadServicios() {
      try {
        const res = await axios.get('http://localhost:3001/servicios')
        this.servicios = res.data
      } catch (error) {
        console.error('Error cargando servicios:', error)
      }
    },
    validate() {
      this.errors = {}

      if (!this.form.nombre.trim()) {
        this.errors.nombre = 'El nombre es obligatorio'
      } else if (this.form.nombre.trim().length < 3) {
        this.errors.nombre = 'El nombre debe tener al menos 3 caracteres'
      }

      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
      if (!this.form.email.trim()) {
        this.errors.email = 'El correo es obligatorio'
      } else if (!emailRegex.test(this.form.email)) {
        this.errors.email = 'Ingresa un correo válido'
      }

      if (!this.form.servicio) {
        this.errors.servicio = 'Selecciona un servicio'
      }

      if (!this.form.mensaje.trim()) {
        this.errors.mensaje = 'El mensaje es obligatorio'
      } else if (this.form.mensaje.trim().length < 10) {
        this.errors.mensaje = 'El mensaje debe tener al menos 10 caracteres'
      }

      return Object.keys(this.errors).length === 0
    },
    async handleSubmit() {
      // Honeypot anti-bots
      if (this.form.honeypot) return

      if (!this.validate()) return

      this.isSubmitting = true

      try {
        await axios.post('http://localhost:3001/contactos', {
          ...this.form,
          honeypot: undefined,
          fecha: new Date().toISOString()
        })

        this.submitSuccess = true
        this.form = { nombre: '', email: '', telefono: '', servicio: '', mensaje: '', honeypot: '' }
        this.errors = {}

        setTimeout(() => { this.submitSuccess = false }, 5000)
      } catch (error) {
        console.error('Error enviando formulario:', error)
      } finally {
        this.isSubmitting = false
      }
    }
  }
}
</script>

<style scoped>
.contact__header {
  background: linear-gradient(135deg, var(--color-primary), var(--color-accent));
  color: white;
  text-align: center;
  padding: 3rem 2rem;
}

.contact__header h1 {
  font-size: 2rem;
  margin-bottom: 0.5rem;
}

.contact__header p {
  opacity: 0.9;
}

.contact__container {
  max-width: 1100px;
  margin: 3rem auto;
  padding: 0 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
}

.form__group {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  margin-bottom: 1.25rem;
}

.form__group label {
  font-weight: 600;
  color: var(--color-primary);
  font-size: 0.95rem;
}

.form__group input,
.form__group select,
.form__group textarea {
  padding: 0.75rem;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
  transition: border-color 0.3s;
  font-family: inherit;
}

.form__group input:focus,
.form__group select:focus,
.form__group textarea:focus {
  outline: none;
  border-color: var(--color-accent);
}

.input--error {
  border-color: #e74c3c !important;
}

.form__error {
  color: #e74c3c;
  font-size: 0.85rem;
}

.form__honeypot {
  display: none;
}

.form__submit {
  width: 100%;
  padding: 0.9rem;
  background-color: var(--color-primary);
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.3s;
}

.form__submit:hover:not(:disabled) {
  background-color: var(--color-accent);
}

.form__submit:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.form__success {
  margin-top: 1rem;
  padding: 1rem;
  background-color: #d4edda;
  color: #155724;
  border-radius: 6px;
  text-align: center;
}

.contact__info h2 {
  color: var(--color-primary);
  margin-bottom: 1.5rem;
  font-size: 1.5rem;
}

.info__item {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
  align-items: flex-start;
}

.info__icon {
  font-size: 1.5rem;
}

.info__item strong {
  display: block;
  color: var(--color-primary);
  margin-bottom: 0.25rem;
}

.info__item p,
.info__item a {
  color: #555;
  font-size: 0.95rem;
  text-decoration: none;
}

.info__item a:hover {
  color: var(--color-accent);
}

.contact__map {
  margin-top: 1.5rem;
}

@media (max-width: 768px) {
  .contact__container {
    grid-template-columns: 1fr;
  }
}
</style>