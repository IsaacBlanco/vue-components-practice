<script setup>
defineProps({
    title:String,
    id: Number,
    body: String
})

const emit = defineEmits(["postFavorito"])

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :id="id">{{ title }}</h5>
            <p>{{body}}</p>
            <button class="btn btn-outline-primary" 
            @click="emit('postFavorito' , title)"
            >Favorito</button>
        </div>
    </div>
</template>