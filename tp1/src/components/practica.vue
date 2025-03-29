<script setup>
import { reactive, ref } from 'vue';

const persona = reactive({
    nombre: '',
    apellido: '',
    edad: ''
});


const animal = reactive({
    tipo: '',
    patas: '',
    alas: '',
    aletas: '',
});

const nombre =ref('');
const apellido=ref('')
const edad=ref('')


</script>

<template>
<input type="text" v-model="persona.nombre" placeholder="Nombre">
<input type="text" v-model="persona.apellido" placeholder="Apellido">
<input type="number" v-model="persona.edad" placeholder="Edad">
<button>Enviar</button>

<p>nombre: {{ persona.nombre }}</p>
<p>apellido: {{ persona.apellido }}</p>
<p>edad: {{ persona.edad }}</p>

</template>

