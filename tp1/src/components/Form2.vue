<script lang="ts" setup>
import { ref } from "vue";


const nombre = ref('');
const mail = ref('');
const pass = ref('');
const fechaNacimiento = ref('');


function calcularEdad(fechaNac: string) {
  if (!fechaNac) return null;
  const fecha = new Date(fechaNac);
  const hoy = new Date();
  let edad = hoy.getFullYear() - fecha.getFullYear();
  const mes = hoy.getMonth() - fecha.getMonth();

  if (mes < 0 || (mes === 0 && hoy.getDate() < fecha.getDate())) {
    edad--;
  }
  return edad;
}

function limpiarCampos() {
  nombre.value = '';
  mail.value = '';
  pass.value = '';
  fechaNacimiento.value = '';
}


function mostrarAlerta() {
  const edad =calcularEdad(fechaNacimiento.value);
  alert(
  `Usuario agregado correctamente\n` +
  `nombre : ${nombre.value}\n` +
  `mail: ${mail.value}\n` +
  `contraseña; ${pass.value}\n` +
  `edad: ${edad !== null ? edad : 'no especificada'}`
  )
}
function guardarDatos() {
  mostrarAlerta();
  limpiarCampos();
}



</script>

<template>
  <form @submit.prevent="guardarDatos">
    <input type="text" placeholder="Nombre de usuario" v-model="nombre"><br>
    <input type="mail" placeholder="Email" v-model="mail"><br>
    <input type="password" placeholder="Constraseña" v-model="pass"><br>
    <input type="date" v-model="fechaNacimiento"><br>
    <button type="submit">Enviar</button>
  </form>
  <div>
    <h3>Datos:</h3><br>
    <p>Nombre: {{ nombre }}</p>
    <p>Mail: {{ mail }}</p>
    <p>Contraseña: {{ pass }}</p>
    <p>Fecha de naciemiento: {{ fechaNacimiento }}</p>
    <p>Edad: {{ calcularEdad(fechaNacimiento) }}</p>

  </div>



</template>

<style scope>
input {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 20px;
  border: 1px solid #ccc;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #423bc7;
  color: white;
  border-radius: 20px;
}

button:hover {
  background-color: #1d1883;
}

div {
  margin-top: 20px;
  font-size: 16px;
}

h3 {
  color: #333;
}
</style>