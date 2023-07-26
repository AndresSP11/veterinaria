<script setup>
    import {reactive} from 'vue';
    const paciente=reactive({
        nombre: '',
        propietario:'',
        email:'',
        fecha:'',
        sintomas:''
    });
    const validar=()=>{
        console.log("validando")
    }
</script>
<template>
    <div class="w-1/2 ml-8">
        <h2 class="font-black text-3xl text-center"> 
            Seguimiento de Pacientes
        </h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>
        <form class="bg-white shadow-xl rounded-lg py-10 px-5 mb-10"
        @submit.prevent="validar">
            <!-- NOMBRE DE LA MASCOTA -->
            {{ paciente.nombre }}
            {{ paciente.fecha }}
            {{ paciente.sintomas }}
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">Nombre de Mascota</label>
                <input 
                v-model="paciente.nombre"
                type="text" class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg" placeholder="Nombre de Mascota" id="mascota"> 
                
            </div>
            <!-- NOMBRE DEL PROPIETARIO -->
            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">Nombre de Propietario</label>
                <input type="text" class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg"
                v-model="paciente.propietario"
                placeholder="Nombre de Propietario" id="propietario"> 
            </div>
            <!-- EMAIL INTRODUCIRLOP -->
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">INTRODUCIR EMAIL</label>
                <input type="email" class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg"
                v-model="paciente.email" 
                placeholder="Introduzca su Email" id="email"> 
            </div>
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">FECHA DE MASCOTA</label>
                <input type="date" class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg" id="mascota"
                v-model="paciente.fecha"> 
            </div>
            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">SINTOMAS</label>
                <textarea  id="sintomas" class=" border-4 w-full p-2 mt-2 h-40 mb-5 placeholder-indigo-600 rounded-lg" placeholder="Sintomas del animal"
                v-model="paciente.sintomas"></textarea>
            </div>
            <input type="submit" value="ENVIAR" class="w-full bg-indigo-700 h-14 rounded-xl text-white font-bold hover:bg-indigo-600 
            cursor-pointer transition-colors">
        </form>
    </div>
</template>