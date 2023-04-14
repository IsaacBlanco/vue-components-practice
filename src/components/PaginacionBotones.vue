<script setup>

defineProps({
    inicio: Number,
    postsLen: Number
})
const emit = defineEmits(["botonSiguiente","botonAnterior"])

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" 
        class="btn btn-primary" 
        :disabled="inicio <= 0"
        @click="emit('botonAnterior')"
        >Anterior {{ inicio }}</button>

        <button type="button" 
        class="btn btn-primary" 
        :disabled="inicio+10 >= postsLen"
        @click="emit('botonSiguiente')"
        >Sigueinte {{ postsLen }}</button>
    </div>


</template>