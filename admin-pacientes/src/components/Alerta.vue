<script setup>
    import {computed} from 'vue'
    const props= defineProps({
        alerta:{
            type:Object,
            required:true
        }
    })
    const isError= computed(()=>{
        if(props.alerta.tipo==='error'){
            return "w-full rounded-md bg-red-600 text-yellow-50 font-bold h-12 text-center p-3 mb-3";
        }else{
            return "w-full rounded-md bg-green-400 text-yellow-50 font-bold h-12 text-center p-3 mb-3"
        }
    })
</script>

<template>
    <div v-if="alerta.mensaje!=''" :class="isError">{{ alerta.mensaje }}</div>
</template>