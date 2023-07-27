<script setup>
    import {computed} from vue
    const props= defineProps({
        alerta:{
            type:Object,
            required:true
        }
    })
    const isError= computed(()=>{
        return "w-full rounded-md bg-red-600 text-yellow-50 font-bold h-12 text-center p-3 mb-3";
    })
</script>

<template>
    <div 
    :class="isError"
    class="w-full rounded-md bg-red-600 text-yellow-50 font-bold h-12 text-center p-3 mb-3">{{ alerta.mensaje }}</div>
</template>