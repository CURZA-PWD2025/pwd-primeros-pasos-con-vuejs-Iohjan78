<template>
    <div class="card">
        <h2>Titulo: {{ movie.titulo }}</h2>
        <p>Id: {{ movie.id }}</p>
        <p>Año: {{ movie.anio }}</p>
        <p>Género: {{ Array.isArray(movie.generos) && movie.generos.length > 0 ? movie.generos.join(', ') : 'No disponible' }}</p>
        <p>Director: {{ movie.director }}</p>
        <div v-if="imagenCargada">
            <img :src="movie.portada" alt="Portada" @error="imagenCargada = false" style="max-width: 200px;" />
        </div>
        <p v-else>PORTADA NO DISPONIBLE</p>
        <p>Likes: {{ movie.likes }}</p>
        <button  @click="meGusta" :class="['botonMeGusta', { activo: likeActivo }]">👍 Me Gusta</button>
    </div>
</template>


<script setup lang="ts">
import { Pelicula } from '../interfaces/Pelicula'
import { ref } from 'vue'


//aqui cardComponent recibe del padre una prop movie con la estructura de pelicula
const props = defineProps<{
  movie: Pelicula
}>()


// aca se realiza un evento llama me_gusta , que cardComponente envio al padre, pasandole un id como dato
const emit = defineEmits<{
  (e: 'me_gusta', id: number): void
}>()


//es una CONSTANTE REACTIVA , inicia como true pero puede cambiar con @error="imagenCargada 
// en v-else>PORTADA NO DISPONIBLE
const imagenCargada = ref(true)

//es una constante reactiva, que da por sentado que no hay un me gusta en el boton
const likeActivo = ref(false)


//se realiza una funcion, que emplea un emit para avisarle al padre el id al cual se le dio click en me gusta
// luego cambia de estado const likeActivo de manera local
function meGusta() {
  emit('me_gusta', props.movie.id)
  likeActivo.value = !likeActivo.value
}
</script>

<style scoped>


.card {
    background: linear-gradient(to bottom, #7feeff, #67a9c6);
    border: solid 2px rgb(0, 0, 0);
    border-radius: 10px;
    padding: 70px;  
    margin: 50px;
}

.botonMeGusta {
  background-color: #c3c3c3;
  color: black;
  transition: background-color 0.3s ease;
}

.botonMeGusta.activo {
  background-color: #0c0fde;
  color: white;
}

</style>