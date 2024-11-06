<template>
  <section class="h-100 gradient-form" style="background-color: #000080;">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-xl-10">
          <div class="card rounded-3 text-black">
            <div class="row g-0">
              <div class="col-lg-6">
                <div class="card-body p-md-5 mx-md-4">

                  <div class="text-center">
                    <img src="@/assets/logo2.jpg" style="width: 185px;" alt="logo"> 
                    <h4 class="mt-1 mb-5 pb-1">Somos Lis Consultas</h4>
                  </div>

                  <form @submit.prevent="login">
                    <p>Ingresa a tu cuenta</p>

                    <div class="form-outline mb-4">
                      <input type="text" v-model="usuario" class="form-control" placeholder="Nombre de usuario" />
                      <label class="form-label" for="form2Example11">Usuario</label>
                    </div>

                    <div class="form-outline mb-4">
                      <input type="password" v-model="clave" class="form-control" />
                      <label class="form-label" for="form2Example22">Clave</label>
                    </div>

                    <div class="text-center pt-1 mb-5 pb-1">
                      <button class="btn btn-primary btn-block fa-lg gradient-custom-2 mb-3" type="submit">Log in</button>
                      <a class="text-muted" href="#!">¿Olvidaste tu clave?</a>
                    </div>

                    <div class="d-flex align-items-center justify-content-center pb-4">
                      <p class="mb-0 me-2">¿No tienes una cuenta?</p>
                      <button type="button" class="btn btn-outline-danger">Crear nueva</button>
                    </div>

                  </form>

                </div>
              </div>
              <div class="col-lg-6 d-flex align-items-center gradient-custom-2">
                <div class="text-white px-3 py-4 p-md-5 mx-md-4">
                  <h4 class="mb-4">Líderes en gestión de información</h4>
                  <p class="small mb-0">Nuestro sistema aporta exactitud y accesibilidad a los flujos de tus muestras y datos del laboratorio clínico.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      usuario: '',
      clave: ''
    };
  },
  methods: {
    login() {
  // Crear el objeto con los datos del formulario
  let datosLogin = {
    usuario: this.usuario,
    clave: this.clave
  };

  // Realizar la petición al servidor para verificar el usuario
  fetch('http://localhost/lisapi/?login', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(datosLogin)
  })
  .then(response => response.json())
  .then(data => {
    if (data.success) {
      // Usuario autenticado correctamente, capturar la id del especialista
      alert("Login exitoso");
      console.log("ID del especialista: ", data.id);
      
      // Puedes almacenar esta id en el localStorage, una variable global, o redirigir a otra página
        localStorage.setItem("especialistaId", data.id);
        let especialistaId = localStorage.getItem("especialistaId");
        console.log(especialistaId)

      // Redirigir a otra página o hacer cualquier otra acción
      window.location.href = '/ListarPacientes';
    } else {
      // Error en la autenticación
      alert("Usuario o clave incorrectos");
    }
  })
  .catch(error => console.log('Error:', error));
}

  }
};
</script>
<style scoped>
.gradient-custom-2 {
  background: linear-gradient(to right, #6aa9e9, #4a7c99);
}
.form-outline input,
.form-outline label,
.text-muted,
p,
button {
  color: #000 !important;
}
button {
  background-color: #0066cc;
  color: white !important;
}
a {
  color: #0066cc !important;
}
@media (min-width: 768px) {
  .gradient-form {
    height: 100vh !important;
  }
  .form-outline input,
  .form-outline label {
    font-size: 1.2rem;
  }
}
@media (min-width: 769px) {
  .gradient-custom-2 {
    border-top-right-radius: .3rem;
    border-bottom-right-radius: .3rem;
  }
}
</style>
