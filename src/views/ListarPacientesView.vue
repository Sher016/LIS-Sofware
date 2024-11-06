<template> 
    <div class="card text-center border border-dark" style="background-color: #fff; margin: 50px; padding: 50px;">
        <div class="card-header border border-danger" style="background:#333;">
            <h1 class="fw-bolder" style="color: #fff;"> Lista de Pacientes </h1>
            <form class="d-flex" @submit.prevent="consultarPacientesDoc">
                <input class="form-control me-2" type="search" placeholder="Ingrese el documento del paciente a buscar" aria-label="Search" v-model="searchQuery">
                <button class="btn btn-outline-success" type="submit">Buscar</button>
            </form>
        </div>
        <div class="card-body">
            <table class="table">
                <thead>
                    <tr>
                        <th>No.</th>
                        <th>Documento</th>
                        <th>Nombre y apellidos</th>
                        <th>Acciones</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(paciente, index) in pacientes" :key="paciente.id">
                        <td scope="row">{{ index + 1 }}</td>
                        <td>{{paciente.doc}}</td>
                        <td>{{paciente.name}} {{paciente.lastname}}</td>
                        <td>
                            <div class="btn-group" role="group" aria-label="Acciones">
                                <router-link :to="{name:'DetallesPacientes' , params:{id:paciente.id}}" class="btn btn-success">Detalle</router-link>
                                <router-link :to="{name:'ActualizarPacientes' , params:{id:paciente.id}}" class="btn btn-info">Editar</router-link>
                                <button type="button" @click="borrarPaciente(paciente.id, paciente.doc)" class="btn btn-danger">Borrar</button>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="card-footer text-body-secondary">
            LisConsultas
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            pacientes: [],
            searchQuery: '',
            especialistaId: null
        };
    },
    created() {
        this.especialistaId = localStorage.getItem('especialistaId');
        console.log('Especialista ID:', this.especialistaId);
        this.consultarPacientes(); 
    },
    methods: {
        consultarPacientes() {
            
            fetch('http://localhost/lisapi/?consultarusuarios=' + this.especialistaId)
                .then(response => response.json())
                .then((data) => {
                    console.log(data);
                    this.pacientes = [];
                    if (typeof data[0].success === 'undefined') {
                        this.pacientes = data;
                    } else {
                        alert("No se encontraron pacientes para este especialista.");
                    }
                })
                .catch(console.log);
        },
        
        borrarPaciente(id, doc) {
            console.log(id);
            fetch('http://localhost/lisapi/?Usuariosborrar=' + id)
                .then(response => response.json())
                .then((data) => {
                    console.log(data);

                    fetch('http://localhost/lisapi/?Pruebasborrar=' + doc)
                        .then(response => response.json())
                        .then(datap => {
                            console.log(datap);
                            this.consultarPacientes(); // Recargar la lista después de borrar
                        });
                })
                .catch(console.log);
        },
        
        consultarPacientesDoc() {
            if (this.searchQuery.trim() === '') {
                window.location.href = 'ListarPacientes';
                return;
            }

            fetch('http://localhost/lisapi/?consultarPacientesdoc=' + this.searchQuery)
                .then(response => response.json())
                .then((data) => {
                    console.log(data);
                    this.pacientes = [];

                    if (data.length === 0 || typeof data[0].success !== 'undefined') {
                        alert("No se encontraron pacientes con la cédula ingresada.");
                    } else {
                        this.pacientes = data;
                    }
                })
                .catch(error => {
                    console.log(error);
                    alert("Ocurrió un error al consultar los pacientes.");
                });
        }
    }
};
</script>
