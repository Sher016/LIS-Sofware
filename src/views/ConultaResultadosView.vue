<template>
  <section class="text-center text-lg-start full-height">
    <div class="container py-4 h-100 d-flex justify-content-center align-items-center">
      <div class="row g-0 align-items-center w-100">
        <div class="col-lg-6 mb-5 mb-lg-0 mx-auto">
          <div class="card cascading-right" style="
              background: hsla(0, 0%, 100%, 0.55);
              backdrop-filter: blur(30px);">
            <div class="card-body p-5 shadow-5 text-center">
              <h2 class="fw-bold mb-5">Consultar resultados</h2>
              <form @submit.prevent="searchId"> 
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model="documentUser" required/>
                  <label class="form-label" for="form3Example4">Documento de Identidad</label>
                </div>
                <button type="submit" class="btn btn-primary btn-block mb-4">Buscar</button>
                <button type="reset" class="btn btn-danger btn-block mb-4">Limpiar</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.full-height {
  height: 100vh; /* Hace que el contenedor ocupe toda la altura de la pantalla */
}

.card {
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(159, 1, 1, 0.2);
  border-radius: 10px;
}

.fw-bold, .form-label {
  color: #0e1011;
}

.form-control {
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(75, 75, 75, 0.1); 
}

section {
  background-image: url('../assets/labsb2.jpg');
  background-size: cover;
  background-position: center;
  height: 100vh; /* Asegura que el section ocupe toda la pantalla */
}

.container {
  height: 100%;
}

@media (min-width: 992px) {
  .cascading-right {
    margin-right: 50px;
  }
}
</style>

<script>
export default {
  data() {
    return {
      userid: null,
      documentUser: ''
    }
  },
  methods: {
    searchId(event) {
      event.preventDefault();
      const url = `http://localhost/lisapi/?consultarPacientesdoc=${this.documentUser}`
      fetch(url, { method: "GET" })
        .then(respuesta => respuesta.json())
        .then((datosRespuesta) => {
          if (datosRespuesta.success === 0 || !datosRespuesta[0]?.id) {
            alert("Usuario no encontrado");
          } else {
            console.log(datosRespuesta);
            this.userid = datosRespuesta[0].id;
            this.$router.push({ name: 'VerResultados', params: { id: this.userid } });
          }
        })
        .catch(console.log);
    }
  }
}
</script>
