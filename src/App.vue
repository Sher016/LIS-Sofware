<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">
          <img src="@/assets/LIS.jpeg" alt="Logo del Lab" class="logo" />
          <span class="brand-text">LIS Consultas</span>
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav ms-auto">
           
            <li class="nav-item" v-if="shouldShow('home')">
              <router-link class="nav-link" to="/home">
                <i class="fas fa-home"></i> Home
              </router-link>
            </li>
           
            <li class="nav-item" v-if="shouldShow('listarPacientes')">
              <router-link class="nav-link" to="/ListarPacientes">
                <i class="fas fa-users"></i> Listar Pacientes
              </router-link>
            </li>
            
            <li class="nav-item" v-if="shouldShow('ingresarPacientes')">
              <router-link class="nav-link" to="/IngresarPacientes">
                <i class="fas fa-user-plus"></i> Ingresar Pacientes
              </router-link>
            </li>
            
            <li class="nav-item" v-if="shouldShow('consultaResultados')">
              <router-link class="nav-link" to="/ConsultaResultados">
                <i class="fas fa-file-medical-alt"></i> Consulta Resultados de Pruebas
              </router-link>
            </li>
       
            <li class="nav-item" v-if="shouldShow('login')">
              <router-link class="nav-link" to="/login">
                <i class="fas fa-sign-in-alt"></i> Login
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <router-view />


    <footer class="footer bg-dark text-light">
      <div class="container">
        <div class="row">
          <div class="col text-center">
            <h5>Contacto</h5>
            <p>Email: contacto@lisconsultas.com</p>
            <p>Teléfono: +57 123 456 7890</p>
          </div>
          <div class="col text-center">
            <h5>Redes Sociales</h5>
            <a href="https://facebook.com" target="_blank">
              <i class="fab fa-facebook fa-lg text-white"></i>
            </a>
            <a href="https://twitter.com" target="_blank">
              <i class="fab fa-twitter fa-lg text-white"></i>
            </a>
            <a href="https://instagram.com" target="_blank">
              <i class="fab fa-instagram fa-lg text-white"></i>
            </a>
          </div>
          <div class="col text-center">
            <h5>Más información</h5>
            <a href="/politicas" class="footer-link">
              <i class="fas fa-user-shield"></i> Políticas de Privacidad
            </a><br />
            <a href="/terminos" class="footer-link">
              <i class="fas fa-file-contract"></i> Términos de Servicio
            </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  methods: {
    shouldShow(link) {
      const currentPath = this.$route.path;

     
      switch (link) {
        case 'home':
          return true; 
        case 'login':
          return currentPath !== '/login'; 
        case 'consultaResultados':
          return currentPath === '/home' || currentPath === '/ConsultaResultados';
        case 'listarPacientes':
          return currentPath === '/IngresarPacientes' || currentPath === '/ListarPacientes';
        case 'ingresarPacientes':
          return currentPath === '/ListarPacientes';
        default:
          return false;
      }
    }
  }
};
</script>

<style scoped>
#app {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
}

.navbar {
  padding: 10px 20px;
}

.navbar-brand {
  font-weight: bold;
  font-size: 1.5rem;
  display: flex;
  align-items: center;
}

.logo {
  width: 50px;
  margin-right: 10px;
}

.brand-text {
  color: #ffffff;
  font-size: 1.2rem;
}

.navbar-nav .nav-link {
  font-weight: bold;
  color: #ffffff;
  margin-right: 20px;
  transition: color 0.3s ease;
}

.navbar-nav .nav-link:hover {
  color: #f39c12;
}

.navbar-nav .router-link-exact-active {
  color: #f39c12;
}

.footer {
  background-color: #343a40;
  color: white;
  padding: 30px 0;
}

.footer h5 {
  margin-bottom: 20px;
}

.footer a {
  color: white;
  margin: 0 10px;
  font-size: 1.1rem;
}

.footer a:hover {
  color: #f39c12;
}
</style>
