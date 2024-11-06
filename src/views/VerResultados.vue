<template>
  <div class="container">
    <div class="bg-image" style="height: 300px;"></div>
    <div class="card mx-4 mx-md-5 shadow-5-strong" style="margin-top: -100px; background: hsla(0, 0%, 100%, 0.8); backdrop-filter: blur(30px);">
      <div class="card">
        <div class="card-header d-flex align-items-center">
          <img src="../assets/logolindo.png" alt="Logo" class="me-3" style="width: 80px; height: 80px;">
          <h3 class="fw-bold">Resultados perfil lípidico</h3>
        </div>
        <div class="card-body">
          <div class="mb-4">
            <h5>Resultados de usuario con id: <span class="fw-normal">{{ $route.params.id }}</span></h5>
            <p><strong>Nombre y apellidos:</strong> <span class="fw-normal">{{ user.name }} {{ user.lastname }}</span></p>
            <p><strong>Documento:</strong> <span class="fw-normal">{{ user.doc }}</span></p>
            <p><strong>Eps id:</strong> <span class="fw-normal">{{ epss[epsIndex]?.eps }}</span></p>
            <p><strong>Género:</strong> <span class="fw-normal">{{ user.gender }}</span></p>
            <p><strong>Edad:</strong> <span class="fw-normal">{{ user.age }}</span></p>
          </div>
          <div class="table-responsive">
            <table class="table">
              <thead>
                <tr>
                  <th>HDL (mg/dL)</th>
                  <th>LDL (mg/dL)</th>
                  <th>TRIG (mg/dL)</th>
                  <th>CHOLT (mg/dL)</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>{{ pacientePrueba.HDL }}</td>
                  <td>{{ pacientePrueba.LDL }}</td>
                  <td>{{ pacientePrueba.TRIG }}</td>
                  <td>{{ pacientePrueba.CHOLT }}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <button @click="goBack" class="btn btn-info">Regresar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {},
      pacientePrueba: {},
      epss: [], // Inicialización de epss
      epsIndex: null // Inicialización de epsIndex
    };
  },
  created() {
    this.getUserid();
    this.getEps();
  },
  methods: {
    getUserid() {
      const url = 'http://localhost/lisapi/?consultar=' + this.$route.params.id;
      fetch(url)
        .then(respuesta => respuesta.json())
        .then(datosRespuesta => {
          console.log('Datos del usuario:', datosRespuesta);
          if (datosRespuesta.length > 0) {
            this.user = datosRespuesta[0];
            this.getPacientePrueba(this.user.doc);
          } else {
            console.error('No se encontraron datos del usuario.');
          }
        })
        .catch(console.log);
    },
    getEps() {
      fetch('http://localhost/lisapi/?consultarEps')
        .then(respuesta => respuesta.json())
        .then(datosRespuesta => {
          console.log(datosRespuesta);

          if (typeof datosRespuesta[0].success === 'undefined') {
            this.epss = datosRespuesta;
          }

          if (this.user.eps) {
            this.epsIndex = parseInt(this.user.eps) - 1;
          }
        })
        .catch(console.log);
    },
    getPacientePrueba(doc) {
      const url = 'http://localhost/lisapi/?consultarpruebas=' + doc;
      fetch(url)
        .then(response => response.json())
        .then(datap => {
          console.log('Datos de las pruebas:', datap);
          if (datap.length > 0) {
            this.pacientePrueba = datap[0];
          } else {
            console.error('No se encontraron datos de pruebas.');
          }
        })
        .catch(console.log);
    },
    goBack() {
      this.$router.go(-1);
    }
  }
};
</script>

<style scoped>
.bg-image {
  background-image: url('../assets/fondo.jpg');
  height: 300px;
  background-size: cover;
  background-position: center;
}

.card-header {
  border: 1px solid #ccc;
  color: #0e1011;
  display: flex;
  align-items: center;
}

.card-header h3 {
  margin: 0;
  font-size: 1.5rem;
}

.card-body h5 {
  font-size: 1.25rem;
  margin-bottom: 1rem;
  color: black;
}

.card-body p {
  font-size: 1rem;
  margin-bottom: 0.5rem;
  color: black;
}

.table th,
.table td {
  text-align: center;
}

.fw-bold {
  font-weight: 700;
  color: black;
}

.fw-normal {
  font-weight: 400;
  color: black;
}
</style>
