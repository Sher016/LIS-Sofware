

<template>
  <div class="home">
    <div class="container text-center mt-5">
  <div class="row align-items-center">
    <!-- Imagen de bienvenida con animación -->
    <div class="col-md-6 position-relative welcome-carousel">
      <img 
        v-for="(image, index) in images" 
        :key="index" 
        :src="image" 
        alt="Bienvenida a LisConsultas" 
        class="img-fluid rounded shadow-lg" 
        :class="{ 'active': activeImageIndex === index }"
      />
    </div>
        <!-- Texto descriptivo en un cuadro -->
    <div class="col-md-6 d-flex align-items-center">
      <div class="custom-edit-card">
        <div class="card-body2">
          <p class="lead">
            LisConsultas es un sistema de gestión de laboratorio diseñado para facilitar la
            administración de pacientes y resultados de pruebas de laboratorio.
          </p>
        </div>
      </div>
    </div>
  </div>

      <!-- Características Principales -->
      <div class="features mt-5">
        <div class="row">
          <div class="col-md-4">
            <div
              class="card text-center mb-4 feature-card"
              @mouseenter="activeDescription = 'patients'"
              @mouseleave="activeDescription = null"
            >
              <div class="card-body">
                <font-awesome-icon :icon="['fas', 'book-medical']" class="icon large-icon" />
                <h5 class="card-title">Listado de pacientes</h5>
              </div>
            </div>
            <div v-if="activeDescription === 'patients'" class="description">
              <p>Accede al listado completo de pacientes, donde podrás visualizar y gestionar sus datos personales y resultados de pruebas.</p>
            </div>
          </div>
          <div class="col-md-4">
            <div
              class="card text-center mb-4 feature-card"
              @mouseenter="activeDescription = 'edit'"
              @mouseleave="activeDescription = null"
            >
              <div class="card-body">
                <font-awesome-icon :icon="['fas', 'user-edit']" class="icon large-icon" />
                <h5 class="card-title">Ingreso y edición de datos</h5>
              </div>
            </div>
            <div v-if="activeDescription === 'edit'" class="description">
              <p>Permite ingresar nuevos datos de pacientes y editar la información existente de manera sencilla.</p>
            </div>
          </div>
          <div class="col-md-4">
            <div
              class="card text-center mb-4 feature-card"
              @mouseenter="activeDescription = 'results'"
              @mouseleave="activeDescription = null"
            >
              <div class="card-body">
                <font-awesome-icon :icon="['fas', 'clipboard-list']" class="icon large-icon" />
                <h5 class="card-title">Consulta de resultados</h5>
              </div>
            </div>
            <div v-if="activeDescription === 'results'" class="description">
              <p>Consulta y visualiza los resultados de pruebas de laboratorio de los pacientes de manera rápida y eficiente.</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Barra de progreso -->
      <div class="progress-section my-5">
        <h3>Proceso de Gestión</h3>
        <div class="progress">
          <div class="progress-bar" role="progressbar" style="width: 75%;" aria-valuenow="75" aria-valuemin="0" aria-valuemax="100">75%</div>
        </div>
      </div>

      <!-- Sección de testimonios -->
<div class="testimonials my-5">
  <h3>Testimonios</h3>
  <div class="row">
    <div class="col-md-4">
      <div class="testimonial text-center">
        <div class="testimonial-image">
          <img src="@/assets/imagen1.jpg" alt="Dr. Juan Pérez" />
        </div>
        <p>"LisConsultas ha transformado nuestra forma de gestionar los resultados de laboratorio. ¡Recomendado!"</p>
        <cite>- Dr. Juan Pérez</cite>
      </div>
    </div>
    <div class="col-md-4">
      <div class="testimonial text-center">
        <div class="testimonial-image">
          <img src="@/assets/imagen2.jpg" alt="Dra. María Gómez" />
        </div>
        <p>"La eficiencia y facilidad de uso de LisConsultas nos ha ahorrado mucho tiempo."</p>
        <cite>- Dra. María Gómez</cite>
      </div>
    </div>
    <div class="col-md-4">
      <div class="testimonial text-center">
        <div class="testimonial-image">
          <img src="@/assets/imagen3.jpg" alt="Lic. Carlos López" />
        </div>
        <p>"Un sistema intuitivo y completo para cualquier laboratorio."</p>
        <cite>- Lic. Carlos López</cite>
      </div>
    </div>
  </div>
</div>

   
      <div class="news-section my-5">
        <div class="row">
          <div class="col-md-6">
            <div class="news-item">
            </div>
          </div>
          <div class="col-md-6">
            <div class="news-item">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import lab1 from '@/assets/lab1.jpeg';
import lab2 from '@/assets/lab2.jpg';
import lab3 from '@/assets/lab3.jpg';

export default {
  name: 'HomeView',
  components: {
    FontAwesomeIcon,
  },
  data() {
    return {
      activeImageIndex: 0, // Almacena el índice de la imagen activa
      images: [lab1, lab2, lab3],
      interval: null, // Almacena el intervalo para cambiar imágenes
    };
  },
  mounted() {
    // Inicia el intervalo cuando el componente se monta
    this.startImageRotation();
  },
  beforeUnmount() {
    // Limpia el intervalo al destruir el componente
    clearInterval(this.interval);
  },
  methods: {
  startImageRotation() {
    this.interval = setInterval(() => {
      // Cambia la imagen activa
      this.activeImageIndex = (this.activeImageIndex + 1) % this.images.length;
    }, 3000); // Cambia la imagen cada 3 segundos (3000 ms)
  },
},
};
</script>

<style scoped>
.home {
  background-color: #e9f0f5; 
  color: #333;
  padding: 20px;
}
.img-fluid {
  max-height: 500px; 
  width: 100%; 
  object-fit: cover; 
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); 
}

.animated-fade {
  animation: fade 5s infinite;
}

@keyframes fade {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.icon {
  margin-right: 8px;
  color: #1c87c9; 
}

.large-icon {
  font-size: 3rem;
  margin-bottom: 10px; 
}

.card {
  border: 1px solid #dee2e6; 
  border-radius: 0.5rem; 
  padding: 20px;
  background-color: #ffffff; 
  color: #333;
  transition: transform 0.3s, box-shadow 0.3s; 
}

.card-body {
  padding: 20px; 
}

.card-body2 {
  padding: 10px; 
  color: #333; 
  font-size: 1rem; 
}

.card:hover {
  transform: scale(1.05); 
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); 
}

.description {
  margin-top: 10px;
  font-size: 1rem;
  color: #666; 
}

.custom-edit-card {
  background-color: #f8f9fa;
  padding: 20px;
  border-radius: 0.5rem;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  height: 100%; /* Hace la tarjeta más alta */
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-body2 p {
  font-style: italic; 
  quotes: "“" "”";
}
.card-body2 p::after {
  content: close-quote;
}
.lead {
    font-size: 1.2rem;
    font-weight: 200; 
    color: #333; 
    margin: 20px 0; 
}

.text-center {
    text-align: center; 
}

.lead:hover {
    color: #007bff; 
    transition: color 0.3s; 
}
.feature-card {
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s, box-shadow 0.3s;
}

.feature-card:hover {
  background-color: #1c87c9; 
  color: #ffffff; 
  transform: scale(1.05); 
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2); /* Sombra */
}
.testimonial-image {
  width: 200px; 
  height: 200px; 
  border-radius: 100%; 
  overflow: hidden; 
  margin: 0 auto; 
  display: flex; 
  align-items: center; 
  justify-content: center; 
}

.testimonial-image img {
  width: 100%; 
  height: auto; 
}
.welcome-carousel {
  position: relative;
  width: 80%;
  height: 400px; /* Fijamos la altura */
  overflow: hidden; /* Ocultamos el exceso */
}

.welcome-carousel img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%; /* Fijamos la altura */
  object-fit: cover; /* Mantenemos la proporción de la imagen */
  opacity: 0;
  transition: opacity 1s ease-in-out;
  z-index: 0;
}

.welcome-carousel img.active {
  opacity: 1;
  z-index: 1;
}
.row.align-items-center {
  display: flex;
  align-items: center;
}

.col-md-8 {
  flex: 0 0 auto;
  width: 40%;
}

.col-md-6 {
  flex: 0 0 auto;
  width: 70%;
  padding-left: 10px; /* Ajustar espacio entre la imagen y el texto */
}

</style>

