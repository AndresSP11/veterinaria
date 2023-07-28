<script setup>
    import {reactive, computed} from 'vue';
    import Alerta from './Alerta.vue';
    const alerta=reactive({
        mensaje:'',
        tipo:''
    })


    const props=defineProps({
        id:{
            type:[String,null],
            required:true
        },
        nombre:{
            type:String,
            required:true
        },
        propietario:{
            type:String,
            required:true
        },
        fecha:{
            type:String,
            required:true
        },
        sintomas:{
            type:String,
            required:true
        },
        email:{
            type:String,
            required:true
        }
        
    })
    const emits = defineEmits(['update:nombre','update:propietario','update:email','update:sintomas','update:fecha','agregar-paciente'])
    const validar=()=>{
        if(Object.values(props).includes('')){
            alerta.mensaje="Llena todo los espacio vacios"
            alerta.tipo="error"
            return
            /* el return es para que vea que si esta vacio ahi muera el arrow fuction y ya no tenga que recorrer al lado de abajo */
        }
        emits('agregar-paciente');
        alerta.mensaje='Paciente Almacenado Correctamente'
        /* alerta.tipo='error' */
        setTimeout(()=>{
            Object.assign(alerta,{
                tipo:'',
                mensaje:''
            })
        },3000)
    }
   const editando=computed(()=>{
        return props.id
   })

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
        <Alerta :alerta="alerta"></Alerta>
        <form class="bg-white shadow-xl rounded-lg py-10 px-5 mb-10"
        @submit.prevent="validar">
            <!-- NOMBRE DE LA MASCOTA -->
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">Nombre de Mascota</label>
                <input 
                :value="nombre"  
                type="text" 
                class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg" 
                placeholder="Nombre de Mascota" 
                id="mascota"
                @input="$emit('update:nombre',$event.target.value)"> 
                
            </div>
            <!-- NOMBRE DEL PROPIETARIO -->
            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold">Nombre de Propietario</label>
                <input 
                type="text" 
                class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg" 
                :value="propietario"
                placeholder="Nombre de Propietario" 
                id="propietario"
                @input="$emit('update:propietario',$event.target.value)" > 
            </div>
            <!-- EMAIL INTRODUCIRLOP -->
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">INTRODUCIR EMAIL</label>
                <input 
                type="email" 
                class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg"
                placeholder="Introduzca su Email" 
                :value="email"
                id="email"
                @input="$emit('update:email',$event.target.value)" > 
            </div>
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold">FECHA DE MASCOTA</label>
                <input 
                type="date" class=" border-4 w-full p-2 mt-2 mb-5 placeholder-indigo-600 rounded-lg"
                id="mascota"
                @input="$emit('update:fecha',$event.target.value)" 
                :value="fecha"
            > 
            </div>
            <div class="mb-5">
                <label for="sintomas" class="block text-gray-700 uppercase font-bold">SINTOMAS</label>
                <textarea  
                
                id="sintomas" 
                class=" border-4 w-full p-2 mt-2 h-40 mb-5 placeholder-indigo-600 rounded-lg" 
                placeholder="Sintomas del animal"
                @input="$emit('update:sintomas',$event.target.value)" 
                :value="sintomas"
                ></textarea>
            </div>
            <input type="submit" :value="[editando ? 'Guardar Cambios' : 'Registrar Cliente']" class="w-full bg-indigo-700 h-14 rounded-xl text-white font-bold hover:bg-indigo-600 
            cursor-pointer transition-colors">
        </form>
    </div>
</template>