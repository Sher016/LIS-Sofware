<template>
   <div style="background-color: #fff; padding: 20px;">
  <!-- Contenedor Flex para alinear la tabla y el botón en el mismo nivel -->
  <div style="display: flex; justify-content: space-between; align-items: center;">
    <!-- Tabla -->
    <table class="table table-borderless rounded-pill" style="background-color: #ffff; max-width: 800px; padding: 20px; color: black; border-color: brown; box-shadow: 0 0px 7px rgba(0, 0, 0, 0.3);margin-left: 30%;">
      <thead>
        <tr>
          <th colspan="6" class="text-center rounded-pill" style="background-color: #f0e9e9;">INFORMACIÓN DEL PACIENTE</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="font-weight: bold;">Nombre Paciente</td>
          <td>{{ paciente.name }} {{ paciente.lastname }}</td>
          <td style="font-weight: bold;">Documento</td>
          <td>{{ paciente.doc }}</td>
          <td style="font-weight: bold;">EPS</td>
          <td>{{ epss[epsIndex]?.epsname }}</td>
        </tr>
        <tr>
          <td style="font-weight: bold;">Género</td>
          <td>{{ paciente.gender }}</td>
          <td style="font-weight: bold;">Edad</td>
          <td>{{ paciente.age }}</td>
        </tr>
      </tbody>
    </table>

   
    <router-link :to="{name:'ListarPacientes'}" class="btn btn-primary" style="background-color: #e32020;margin-right: 10%;" type="submit">
      Volver a Listar Pacientes
      <br><br>
      <i class="fa-solid fa-rotate-right"></i> <i class="fas fa-users"></i>
    </router-link>
  </div>

  
      
 
      <div class="accordion accordion-flush" id="accordionFlushExample" style="max-width: 1000px; margin: auto; padding-top: 20px;">
        <div v-for="(item, index) in pacientePrueba" :key="index" class="accordion-item border border-5 rounded shadow-sm mb-3 bg-white">
          <h2 class="accordion-header" :id="'panelsStayOpen-heading' + index">
            <button class="accordion-button" type="button" style="background-color: #f0e9e9; color: white;" 
                    :data-bs-toggle="'collapse'" 
                    :data-bs-target="'#panelsStayOpen-collapse' + index" 
                    aria-expanded="true" 
                    :aria-controls="'panelsStayOpen-collapse' + index">
              <h5 style="color: black;"><b>Registro Número: {{ index + 1 }}</b></h5>
            </button>
          </h2>
          <div :id="'panelsStayOpen-collapse' + index" class="accordion-collapse collapse show" :aria-labelledby="'panelsStayOpen-heading' + index">
            <div class="accordion-body">
              <h4 class="fw-bold">Perfil Lipídico</h4>
              <div class="perfil-lipidico">
                <table class="table table-bordered">
                  <thead class="table-light">
                    <tr>
                      <th>Prueba</th>
                      <th>Descripción</th>
                      <th>Valor</th>
                      <th>Unidad</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td><strong>Colesterol Total (CHOLT)</strong></td>
                      <td>Mide la cantidad total de colesterol en la sangre.</td>
                      <td>{{ item.CHOLT }}</td>
                      <td>mg/dL</td>
                    </tr>
                    <tr>
                      <td><strong>Lipoproteínas de Alta Densidad (HDL)</strong></td>
                      <td>Conocido como el colesterol bueno, ayuda a eliminar el colesterol de las arterias.</td>
                      <td>{{ item.HDL }}</td>
                      <td>mg/dL</td>
                    </tr>
                    <tr>
                      <td><strong>Lipoproteínas de Baja Densidad (LDL)</strong></td>
                      <td>Conocido como el colesterol malo, puede acumularse en las arterias.</td>
                      <td>{{ item.LDL }}</td>
                      <td>mg/dL</td>
                    </tr>
                    <tr>
                      <td><strong>Triglicéridos (TRIG)</strong></td>
                      <td>Representa un tipo de grasa en la sangre.</td>
                      <td>{{ item.TRIG }}</td>
                      <td>mg/dL</td>
                    </tr>
                    <tr>
                      <td></td>
                      <td></td>
                      <td>
                        <span><router-link :to="{name:'ActualizarPruebasPacientes', params:{id:item.id}}" class="btn btn-success">Editar</router-link></span>
                      </td>
                      <td>
                        <span><button type="button" v-on:click="borrarPaciente(item.id)" class="btn btn-danger">Borrar</button></span>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div><br><br>
      </div>
    </div>
  </template>

<style>
.perfil-lipidico table {
 width: 100%;
 border-collapse: collapse;
 margin-top: 20px;
}

.perfil-lipidico th, .perfil-lipidico td {
 border: 1px solid #ffffff;
 padding: 8px;
 text-align: left;
}

.perfil-lipidico th {
 background-color: #ffffff;
}
</style>

<script>


export default {
  data() {
    return {
      paciente: {},
      pacientePrueba: [],
      epss: [], 
      epsIndex: null 
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
        .then(data => {
          console.log(data);
          this.paciente = data[0];

          fetch('http://localhost/lisapi/?consultarpruebas=' + this.paciente.doc)
            .then(response => response.json())
            .then(datap => {
              console.log(datap);
              this.pacientePrueba = datap;
            });
        })
        .catch(console.log);
    },
    borrarPaciente(id) {
      console.log(id);
      fetch('http://localhost/lisapi/?Pruebasborrar=' + id)
        .then(response => response.json())
        .then(data => {
          console.log(data);
          console.log(id);
          window.location.href = '/ListarPacientes';
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

         
          if (this.paciente.eps) {
            this.epsIndex = parseInt(this.paciente.eps) - 1;
          }
        })
        .catch(console.log);
    }
  }
};



</script>
