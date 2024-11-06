<template>
  <section class="text-center text-lg-start" style="background-color: #2a6db5;">
    <div class="container-fluid">
      <div class="row g-0 align-items-center">
        <!-- Columna izquierda: Formulario de edición de las pruebas -->
        <div class="col-lg-6 left-column">
          <div class="card cascading-right" style="margin-right: 20%;">
            <div class="card-body p-5 shadow-5 text-center">
              <i class="fa-solid fa-flask-vial"></i>
              <h2 class="fw-bold mb-5 custom-title">Editar Pruebas
                <i class="fa-solid fa-flask-vial" style="color: #2a6db5;"></i>
              </h2>
              <form v-on:submit.prevent="actualizarPruebas">
                <div class="row">
                  <div class="col-md-6 mb-4">
                    <div class="form-outline mb-4">
                      <input v-model="pruebaone.HDL" required type="text" class="form-control" aria-label="HDL input" />
                      <label class="form-label">HDL (mg/dL)</label>
                    </div>
                  </div>

                  <div class="col-md-6 mb-4">
                    <div class="form-outline mb-4">
                      <input v-model="pruebaone.LDL" required type="text" class="form-control" aria-label="LDL input" />
                      <label class="form-label">LDL (mg/dL)</label>
                    </div>
                  </div>

                  <div class="col-md-6 mb-4">
                    <div class="form-outline mb-4">
                      <input v-model="pruebaone.TRIG" required type="text" class="form-control" aria-label="TRIG input" />
                      <label class="form-label">TRIG (mg/dL)</label>
                    </div>
                  </div>

                  <div class="col-md-6 mb-4">
                    <div class="form-outline mb-4">
                      <input v-model="pruebaone.CHOLT" required type="text" class="form-control" aria-label="CHOLT input" />
                      <label class="form-label">CHOLT (mg/dL)</label>
                    </div>
                  </div>
                </div>

                <button type="submit" class="btn btn-success">Guardar</button>
              <router-link :to="{name:'ListarPacientes'}" class="btn btn-info" >Cancelar</router-link>
              </form>
            </div>
          </div>
        </div>

        <div class="col-lg-6 right-column">
          <img src="@/assets/imageneditarpruebas.jpg" alt="Imagen del laboratorio" class="img-fluid w-100 h-100" style="object-fit: cover;">
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      pruebaone: {} // Se mantiene en un solo objeto para contener las pruebas
    };
  },
  created() {
    this.obtenerPruebasID();
    
  },
  methods: {
    obtenerPruebasID() {
      fetch('http://localhost/lisapi/?consultarpruebasid=' + this.$route.params.id)
        .then(response => response.json())
        .then((data) => {
          this.pruebaone = data[0]; // Asignamos directamente al objeto
          console.log(this.pruebaone);
        })
        .catch(console.log);
    },
    actualizarPruebas() {
      fetch('http://localhost/lisapi/?actualizarprue', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json' // Especificar el tipo de contenido JSON
        },
        body: JSON.stringify(this.pruebaone) // Enviar las pruebas actualizadas
      })
        .then(response => response.json())
        .then((data) => {
          console.log(data);
          if (data.success) { 
            window.location.href = '/ListarPacientes'; // Redirigir tras la actualización
          } else {
            console.log('Error en la actualización:', data);
          }
        })
        .catch(error => console.log('Error al actualizar:', error));
    }
  }
};
</script>

<style scoped>
.img-fluid {
  height: 100vh;
  object-fit: cover;
}
.card {
  border: 1px solid #766b6b;
  box-shadow: 0 0 50px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  background-color: white;
  max-width: 600px;
  margin: 0 auto;
}
.form-control {
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 70px rgba(75, 75, 75, 0.1);
}
label {
  color: #01050a;
}
.custom-title {
  color: #0a0231;
}
.left-column {
  background-color: #1f3b4d;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.right-column {
  background-color: #dcecfb;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
