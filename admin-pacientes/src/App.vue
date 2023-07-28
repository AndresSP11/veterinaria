<script setup>
import { ref, reactive, watch,onMounted} from 'vue';
import Header from './components/Header.vue'
import Formulario from './components/Formulario.vue'
import Paciente from './components/pACIENTE.VUE'
import {uid} from 'uid'
import pACIENTEVUE from './components/pACIENTE.VUE';

const pacientes=ref([]);
const paciente=reactive({
        id:null,
        nombre: '',
        propietario:'',
        email:'',
        fecha:'',
        sintomas:''
    });

    watch(pacientes,()=>{
        guardarLocalStorage()
    },{
        deep:true
    })

    const guardarLocalStorage=()=>{
        localStorage.setItem('pacientes',JSON.stringify(pacientes.value))
    }
    onMounted(()=>{
        const pacientesStorage=localStorage.getItem('pacientes');
        if(pacientesStorage){
            pacientes.value=JSON.parse(pacientesStorage)
        }
    })
const agregarPaciente=()=>{
    if(paciente.id){
        const { id }=paciente;
        const i = pacientes.value.findIndex((pacienteState)=>pacienteState.id===id)
        pacientes.value[i]={...paciente}
        console.log("Edicion")
    }else{
        console.log("registro nuevo")
        pacientes.value.push({
        ...paciente,
        id: uid()
    });
    }
    
    Object.assign(paciente,{
        nombre:'',
        propietario:'',
        email:'',
        fecha:'',
        sintomas:'',
        id:null
    })
}
const actualizarPaciente=(id)=>{
    const pacienteEditar= pacientes.value.filter(paciente => paciente.id===id)[0]
    console.log(pacienteEditar)
    /* AQUI LE ESTA ASIGNANDO DE NUEVO LOS VALORES DEL INPUT RECORDAR QUE LSO INPUT TIENEN UN :VALUE */
    Object.assign(paciente,pacienteEditar)
}
const eliminarPaciente=(id)=>{
    pacientes.value=pacientes.value.filter(paciente=>paciente.id!==id)
}
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
            v-model:sintomas="paciente.sintomas"
            @agregar-paciente="agregarPaciente"
            :id="paciente.id"

            ></Formulario>
            <div class=" md:w-1/2 md:h-screen overflow-y-scroll">
                <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
                <div v-if="pacientes.length>0">
                    <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
                 </p>
                    <Paciente v-for="paciente in pacientes"
                    :paciente="paciente"
                    @actualizar-paciente="actualizarPaciente"
                    @eliminar-paciente="eliminarPaciente"></Paciente>
                </div>
                <p v-else class="mt-20 text-2xl text-center text-blue-80">NO HAY PACIENTES</p>
                
            </div>
        </div>
    </div>
</template>


