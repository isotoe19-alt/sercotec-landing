# 🏢 Centro de Negocios Santiago - SERCOTEC

Landing page desarrollada con Vue.js + Vite para el Centro de Negocios Santiago de SERCOTEC.

## 🚀 Tecnologías utilizadas

- **Vue.js 3** - Framework frontend
- **Vite** - Bundler y servidor de desarrollo
- **Vue Router 4** - Enrutamiento
- **Axios** - Consumo de API
- **JSON Server** - API REST mock

## 📁 Estructura del proyecto
sercotec-landing/
├── src/
│   ├── assets/
│   │   ├── css/
│   │   │   └── main.css        # Estilos globales y variables CSS
│   │   └── images/             # Imágenes del proyecto
│   ├── components/
│   │   ├── NavBar.vue          # Navegación principal
│   │   ├── Footer.vue          # Pie de página
│   │   ├── ServiceCard.vue     # Tarjeta de servicio reutilizable
│   │   └── TestimonialCarousel.vue  # Carrusel de testimonios
│   ├── views/
│   │   ├── HomeView.vue        # Página principal
│   │   └── ContactView.vue     # Página de contacto
│   ├── router/
│   │   └── index.js            # Configuración de rutas
│   ├── data/
│   │   └── db.json             # Base de datos mock (JSON Server)
│   ├── App.vue                 # Componente raíz
│   └── main.js                 # Punto de entrada
├── public/                     # Archivos estáticos
├── package.json
└── vite.config.js
## ⚙️ Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/isotoe19-alt/sercotec-landing.git
cd sercotec-landing
```

2. Instala las dependencias:
```bash
npm install
```

3. Inicia el servidor de la API (JSON Server):
```bash
npx json-server src/data/db.json --port 3001
```

4. En otra terminal, inicia el servidor de desarrollo:
```bash
npm run dev
```

5. Abre el navegador en `http://localhost:5174`

## 🧩 Componentes desarrollados

### ServiceCard
Tarjeta de servicio reutilizable que muestra imagen, título, descripción y botón de contacto.

**Props:**
| Prop | Tipo | Requerido | Descripción |
|------|------|-----------|-------------|
| service | Object | Sí | Objeto con id, titulo, descripcion, imagen |

**Ejemplo de uso:**
```vue
<ServiceCard :service="{ id: 1, titulo: 'Asesoría', descripcion: 'Texto...', imagen: 'url' }" />
```

### TestimonialCarousel
Carrusel responsive de testimonios con autoplay, navegación por botones y puntos indicadores.

**Props:**
| Prop | Tipo | Requerido | Descripción |
|------|------|-----------|-------------|
| testimonials | Array | Sí | Lista de testimonios |

**Ejemplo de uso:**
```vue
<TestimonialCarousel :testimonials="testimonials" />
```

## 🌐 Endpoints API

El proyecto usa JSON Server como CMS. Los endpoints disponibles son:

| Endpoint | Método | Descripción |
|----------|--------|-------------|
| `/servicios` | GET | Lista de servicios |
| `/testimonios` | GET | Lista de testimonios |
| `/faqs` | GET | Preguntas frecuentes |
| `/nosotros` | GET | Información institucional |
| `/contactos` | POST | Envío de formulario de contacto |

## 🌿 Ramas del proyecto

| Rama | Descripción |
|------|-------------|
| `main` | Rama principal |
| `feature/componentes` | Desarrollo de componentes reutilizables |
| `feature/carrusel` | Componente carrusel de testimonios |
| `feature/formulario-contacto` | Formulario de contacto con validación |
| `feature/buenas-practicas` | Guía de buenas prácticas |

## ✅ Buenas prácticas implementadas

1. **Nomenclatura PascalCase** para componentes Vue
2. **Nomenclatura kebab-case** para archivos CSS y clases
3. **Props validadas** con tipos y validadores
4. **Accesibilidad** con atributos ARIA y roles semánticos
5. **Lazy loading** en imágenes con `loading="lazy"`
6. **Variables CSS** para colores y temas consistentes
7. **Componentes reutilizables** con props bien definidas
8. **Validación de formularios** del lado del cliente
9. **Protección honeypot** contra bots en formularios
10. **Responsive design** con media queries

## 👥 Integrantes del equipo

- IGNACIO SOTO


## 📄 Licencia

Proyecto educativo - Instituto Profesional San Sebastián