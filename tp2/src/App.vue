<script setup lang="ts">

import cardComponent from './components/cardComponent.vue'
//import movies from './resources/movies'
import { Pelicula } from './interfaces/Pelicula'
import { ref, } from 'vue'
import movieData from './resources/movies'


//se crea una variable reactiva haciendo una copia de los datos para que no se vean 
// alterados los valores originales
const movies =ref<Pelicula[]>([...movieData])


//crea una estructura clave valor con los likes de las peliculas, es para comparar los likes si fue alterado
const baseMeGusta =new Map <number,number>()
movieData.forEach(p => baseMeGusta.set(p.id, p.likes))


//toma el id proveniente del emit, trae el numero de like de Map, se asegura que el id 
// y el numero de likes es valido, y si verifica si toca el botton para sumar el like o no
function variante_megusta (id: number) {
  const pelicula =movies.value.find(p=>p.id === id)
  const base =baseMeGusta.get(id)

  if (pelicula && typeof base === 'number') {
    pelicula.likes = pelicula.likes === base ? pelicula.likes +1 : base
  }
}


</script>

<template>
  <cardComponent
    v-for="(pelicula, index) in movies"
    :key="index"
    :movie="pelicula" 
    @me_gusta="variante_megusta"
    />
</template>

<style scoped>

</style>
