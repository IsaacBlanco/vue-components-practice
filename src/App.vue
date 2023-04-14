<script setup>
import { onMounted, ref } from 'vue';


import BlogPost from './components/BlogPost.vue';
import PaginacionBotones from './components/PaginacionBotones.vue'
import LoadingSpinner from './components/LoadingSpinner.vue';

const posts =ref([]);
const favorito = ref('')
const inicio = ref(0)
const spinner = ref(true)


const postFavorito = (title) => {
  favorito.value = title
  console.log(inicio)
}
const botonSiguiente = () =>{
  inicio.value += 10
  console.log(inicio.value)
}
const botonAnterior = () =>{
  inicio.value -= 10
  console.log(inicio.value)
}

onMounted(async()=>{
  try{
    const respuesta = await fetch("https://jsonplaceholder.typicode.com/posts")
    posts.value = await respuesta.json();
  }catch(e){
    console.log(e)
  }finally{
    setTimeout(() => {
      spinner.value = false
    }, 2000)
  }
})



/* fetch("https://jsonplaceholder.typicode.com/posts")
.then((response) => response.json())
.then((data) => posts.value = data)
.catch((e) => console.log(e))
.finally(() =>{
    setTimeout(() => {
      spinner.value = false
    }, 2000)
}) */


</script>

<template>

  <LoadingSpinner v-if="spinner"></LoadingSpinner>
  <div v-else class="container">
    <h1 class="mt-5">APP</h1>
    <h2 class="mt-3">Mi Post Favorito: {{ favorito }}</h2>

    <PaginacionBotones class="mb-2"
    :inicio = "inicio"
    :postsLen = "posts.length"
    @botonSiguiente = "botonSiguiente"
    @botonAnterior = "botonAnterior"></PaginacionBotones>

    <BlogPost v-for="post in posts.slice(inicio, inicio+10)"
        :key="post.id"
        :title="post.title"
        :id="post.id"
        :body="post.body"
        @postFavorito = "postFavorito"
        class="mb-2"
    ></BlogPost>
   
  </div>
</template>