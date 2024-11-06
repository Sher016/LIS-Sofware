<template> 
  <section class="text-center text-lg-start" style="background-color: #2a6db5;">
    <div class="container-fluid">
      <div class="row g-0 align-items-center">
        <!-- Columna izquierda: Formulario de edición del paciente -->
        <div class="col-lg-6 left-column">
          <div class="card cascading-right" style="margin-right: 20%;">
            <div class="card-body p-5 shadow-5 text-center">
              <i class="fa-solid fa-user-pen"></i>
              <h2 class="fw-bold mb-5 custom-title">Editar Paciente
                <i class="fa-solid fa-user-pen" style="color: #2a6db5;"></i>
              </h2>
              <form v-on:submit.prevent="actualizarPaciente">
                <div class="row">
                  <div class="col-md-6 mb-4">
                    <div class="form-outline">
                      <input type="text" id="form3ExampleName" class="form-control" v-model="nameUser" required />
                      <label class="form-label" for="form3ExampleName">Nombres</label>
                    </div>
                  </div>
                  <div class="col-md-6 mb-4">
                    <div class="form-outline">
                      <input type="text" id="form3ExampleLastName" class="form-control" v-model="lastnameUser" required />
                      <label class="form-label" for="form3ExampleLastName">Apellidos</label>
                    </div>
                  </div>
                </div>
                <div class="form-outline mb-4">
                  <input type="tel" id="form3ExampleDocument" class="form-control" v-model="documentUser" required />
                  <label class="form-label" for="form3ExampleDocument">Documento de Identidad</label>
                </div>
                <div class="form-outline mb-4">
                  <input type="tel" id="form3ExampleAge" class="form-control" v-model="age" required />
                  <label class="form-label" for="form3ExampleAge">Edad</label>
                </div>
                <div class="form-outline mb-4">
                  <select class="form-select" id="form3ExampleGender" v-model="Gender" required>
                    <option v-for="gender in genders" :key="gender" :value="gender">{{ gender }}</option>
                  </select>
                  <label class="form-label" for="form3ExampleGender">Género</label>
                </div>
                <div class="form-outline mb-4">
                  <select class="form-select" id="form3ExampleEps" v-model="epsName" required>
                    <option v-for="eps in epss" :key="eps.epsname" :value="eps.epsname">{{ eps.epsname }}</option>
                  </select>
                  <label class="form-label" for="form3ExampleEps">EPS</label>
                </div>
                <div class="btn-group" role="group" aria-label="">
                  <button type="submit" class="btn btn-success">Guardar</button>
                  <router-link :to="{ name: 'ListarPacientes' }" class="btn btn-danger">Cancelar</router-link>
                </div>
              </form>
            </div>
          </div>
        </div>
        <!-- Columna derecha: Imagen -->
        <div class="col-lg-6 right-column">
          <img src="@/assets/imageneditar.jpg" alt="Imagen del laboratorio" class="img-fluid w-100 h-100" style="object-fit: cover;">
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      nameUser: '',
      lastnameUser: '',
      documentUser: '',
      age: '',
      Gender: '',
      epsName: '',
      genders: ["Masculino", "Femenino"],
      epss: [],
    };
  },
  created() {
    this.obtenerPacienteID();
    this.getEps();
  },
  methods: {
    obtenerPacienteID() {
      fetch('http://localhost/lisapi/?consultar=' + this.$route.params.id)
        .then(response => response.json())
        .then((data) => {
          let paciente = data[0];
          this.nameUser = paciente.name;
          this.lastnameUser = paciente.lastname;
          this.documentUser = paciente.doc;
          this.age = paciente.age;
          this.Gender = paciente.gender;
          this.epsName = paciente.eps;
        })
        .catch(console.log);
    },
    getEps() {
      fetch('http://localhost/lisapi/?consultarEps')
        .then(respuesta => respuesta.json())
        .then((datosRespuesta) => {
          if (typeof datosRespuesta[0].success === 'undefined') {
            this.epss = datosRespuesta;
          }
        })
        .catch(console.log);
    },
    actualizarPaciente() {
  let datosPaciente = {
    id: this.$route.params.id,
    doc: this.documentUser,
    name: this.nameUser,
    lastname: this.lastnameUser,
    age: this.age,
    gender: this.Gender,
    eps: this.epsName
  };
  

  fetch('http://localhost/lisapi/?actualizar', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json' // Añadimos el tipo de contenido para asegurarnos de que el servidor lo interprete bien
    },
    body: JSON.stringify(datosPaciente)
  })
    .then(response => response.json())
    .then((data) => {
      console.log(data);
      if (data.success) { // Si la actualización es exitosa
        window.location.href = '/ListarPacientes';
      } else {
        console.log('Error en la actualización:', data);
      }
    })
    .catch(error => console.log('Error al actualizar:', error));
    },

    
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
