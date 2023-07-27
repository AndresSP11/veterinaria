<script setup>
    import {computed} from 'vue'
    const props= defineProps({
        alerta:{
            type:Object,
            required:true
        }
    })
    /* const isError= computed(()=>{
        if(props.alerta.tipo=="error"){
            return "bg-red-600"
        }else{
            return "bg-green-400"
        }
    }) */
</script>

<template>
    <div 
    class="w-full rounded-md text-yellow-50 font-bold h-12 text-center p-3 mb-3">{{ alerta.mensaje }}</div>
</template>