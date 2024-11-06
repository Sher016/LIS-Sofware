<template> 

  <section class="text-center text-lg-start">
    <!-- Jumbotron -->
    <div class="container py-4">
      <div class="row g-0 align-items-center">
        <div class="col-lg-6 mb-5 mb-lg-0">
          <div class="card cascading-right">
            <div class="card-body p-5 shadow-5 text-center">
              <h2 class="fw-bold mb-5 custom-title">Crear usuario</h2>
              <form>
              <div class="row">
                  <div class="col-md-6 mb-4">
                    <div class="form-outline">
                      <input type="text" id="form3Example1" class="form-control" v-model="nameUser" required/>
                      <label class="form-label" for="form3Example1">Nombres</label>
                    </div>
                  </div>
                  <div class="col-md-6 mb-4">
                    <div class="form-outline">
                      <input type="text" id="form3Example2" class="form-control" v-model="lastnameUser" required/>
                      <label class="form-label" for="form3Example2">Apellidos</label>
                    </div>
                  </div>
                </div>
                
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model="documentUser" required/>
                  <label class="form-label" for="form3Example4">Documento de Identidad</label>
                </div>
  
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model="age" required/>
                  <label class="form-label" for="form3Example4">Edad</label>
                </div>
  
                <div class="form-outline mb-4">
                  <select class='form-select'  id="form3Example4" v-model="Gender" required>
                    <option v-for="gender in genders" :key=" gender " :value=" gender "> {{ gender }} </option>
                  </select>
                  <label class="form-label" for="form3Example4"> Género </label>
                </div>
  
  
                <div class="form-outline mb-4">
                  <select class='form-select'  id="form3Example4" v-model="epsName" required>
                    <option v-for="eps in epss" :key="eps.id" :value="eps.id"> {{ eps.epsname }} </option>
                  </select>
                  <label class="form-label" for="form3Example4"> Eps </label>
                </div>
  
                <div class="row">
                  <div class="col-md-6 mb-4">
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model=" hdl " required/>
                  <label class="form-label" for="form3Example4">HDL (mg/dL)</label>
                </div>
  
                </div>
  
                  <div class="col-md-6 mb-4">
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model="ldl" required/>
                  <label class="form-label" for="form3Example4">LDL (mg/dL)</label>
                </div>
  
                </div>
                  <div class="col-md-6 mb-4">
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model="trig" required/>
                  <label class="form-label" for="form3Example4">TRIG (mg/dL)</label>
                </div>
  
                </div>
  
                  <div class="col-md-6 mb-4">
                <div class="form-outline mb-4">
                  <input type="tel" id="form3Example4" class="form-control" v-model="cholt" required/>
                  <label class="form-label" for="form3Example4">CHOLT (mg/dL)</label>
                </div>
                </div>
                  <!-- Formularios adicionales que aparecen al hacer clic en "Agregar otra prueba" -->
    <div v-for="(prueba, index) in pruebas.slice(1)" :key="index" class="col-12">
      
      <h3 style="color: #01050a;">Nueva Prueba</h3>
      <div class="row">
        <div class="col-md-6 mb-4">
          <div class="form-outline mb-4">
            <input type="tel" class="form-control" v-model="prueba.hdl" required />
            <label class="form-label">HDL (mg/dL)</label>
          </div>
        </div>
        <div class="col-md-6 mb-4">
          <div class="form-outline mb-4">
            <input type="tel" class="form-control" v-model="prueba.ldl" required />
            <label class="form-label">LDL (mg/dL)</label>
          </div>
        </div>
        <div class="col-md-6 mb-4">
          <div class="form-outline mb-4">
            <input type="tel" class="form-control" v-model="prueba.trig" required />
            <label class="form-label">TRIG (mg/dL)</label>
          </div>
        </div>
        <div class="col-md-6 mb-4">
          <div class="form-outline mb-4">
            <input type="tel" class="form-control" v-model="prueba.cholt" required />
            <label class="form-label">CHOLT (mg/dL)</label>
          </div>
        </div>
      </div>
    </div>
  </div>
  <button type="button" class="btn btn-secondary btn-block mb-4" @click="agregarPrueba">Agregar otra prueba </button>
                <button type="submit" class="btn btn-primary btn-block mb-4" @click="SaveUser">
                  Crear
                </button>
                <button type="reset" class="btn btn-danger btn-block mb-4">
                 Limpiar
               </button>                      
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Jumbotron -->
  </section>
  <!-- Section: Design Block -->
  </template>
  
  <style scoped>
  .card {
    border: 1px solid #ccc;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    border-radius: 10px;
    background-color: rgba(255, 255, 255, 0.8);
  }
  
  .form-control {
    border: 1px solid #ccc;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(75, 75, 75, 0.1);
  }
  label {
  color: #01050a; 
  }
  .custom-title {
  color: #0a0231; 
  }
  
  section {
    padding-top: 5%; 
    background-image: url('../assets/labsb2.jpg');
    background-size: cover;
    background-position: center;
    padding-bottom: 5%;
  }
  
  @media (min-width: 992px) {
    .cascading-right {
      margin-right: 50px;
    }
  }
  </style>
  
  <script>
  export default{
    data(){
          return {
              genders:["Masculino","Femenino"]
              ,epss:[],
              nameUser: '',
              lastnameUser: '',
              documentUser: '',
              age: '',
              gender: '',       
              epsName: '',
              hdl: '',
              ldl: '',
              trig: '',
              cholt: '',
              pruebas: [{ hdl: '', ldl: '', trig: '', cholt: '' }],
              especialistaId: null,
          }
      },
      created:function(){
         this.getEps() ,
         this.especialistaId = localStorage.getItem('especialistaId')
      },
  methods:{
    agregarPrueba() {
      this.pruebas.push({ hdl: '', ldl: '', trig: '', cholt: '' });
    },
    
         SaveUser(){
        const name= this.nameUser
        const lastname=this.lastnameUser
        const document= encodeURIComponent(this.documentUser)
        const age= encodeURIComponent(this.age)
        const gender=encodeURIComponent(this.Gender) 
        const eps=encodeURIComponent(this.epsName)  
        const hdl=encodeURIComponent(this.hdl)
        const ldl=encodeURIComponent(this.ldl)
        const trig=encodeURIComponent(this.trig)
        const cholt=encodeURIComponent(this.cholt)
        const especialistaId = this.especialistaId;  
     
        let enviar={
          "doc":document,
          "name":name,
          "lastname":lastname,
          "age":age,
          "gender":gender,
          "eps":eps,
          "hdl":hdl,
          "ldl":ldl,
          "trig":trig,
          "cholt": cholt,
         "id_especialista" :especialistaId
        }
      console.log(JSON.stringify(enviar))
       fetch('http://localhost/lisapi/?insertar',{
                  method:"POST",
                  body:JSON.stringify(enviar)
              })
              .then(respuesta=>respuesta.json())
              .then((datosRespuesta=>{
                  console.log(datosRespuesta);
              }))
              .catch((error=>{console.error("Error:",error);
              alert("ERROR EN ENVIO DE DATOS DE USUARIO")})) 
              //enviar usuarios a la tabla pruebas de la misma forma como se envia a usuarios              
               let enviarPrueba = {
                  "doc": document,
                  "id_especialista": especialistaId, 
                  "hdl": hdl, 
                  "ldl": ldl, 
                  "trig": trig,
                  "cholt": cholt 
              };
          console.log(JSON.stringify(enviarPrueba));
          fetch('http://localhost/lisapi/?insertarPrueba', {
                  method: "POST",
                  body: JSON.stringify(enviarPrueba) 
              })
              .then(respuesta => respuesta.json())
              .then((datosRespuesta => {
              console.log(datosRespuesta);
              }))
              .catch((error => {console.error("Error:", error);
              alert("ERROR EN ENVIO DE PRUEBAS")}));
            },
        getEps(){
          fetch('http://localhost/lisapi/?consultarEps')
          .then(respuesta=>respuesta.json())
                    .then((datosRespuesta)=>{
                        console.log(datosRespuesta)
                        this.epss=[]
                        if(typeof datosRespuesta[0].success==='undefined'){
                            this.epss=datosRespuesta;
                        }
  
                    })
                    .catch(console.log)
      }
  
      
  }
  }
  
  </script>