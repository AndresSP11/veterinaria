<script setup>
import { ref, reactive} from 'vue';
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
const pacientes=ref([]);
const paciente=reactive({
        nombre: '',
        propietario:'',
        email:'',
        fecha:'',
        sintomas:''
    });
</script>

<template>
    <div class="container mx-auto mt-10">
        
        <Header></Header>
        <div class="mt-12 flex ml-12 mx-5">
            <Formulario
            v-model:nombre="paciente.nombre"
            v-model:propietario="paciente.propietario"
            v-model:email="paciente.email"
            v-model:fecha="paciente.fecha"
            v-model:sintomas="paciente.sintomas"></Formulario>
            <div class=" md:w-1/2 md:h-screen overflow-y-scroll">
                <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
                <div v-if="pacientes.length>0">
                
                </div>
                <p v-else class="mt-20 text-2xl text-center text-blue-80">NO HAY PACIENTES</p>
            </div>
        </div>
    </div>
</template>


