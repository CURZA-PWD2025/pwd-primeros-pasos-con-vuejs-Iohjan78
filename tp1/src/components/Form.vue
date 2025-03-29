<script>
export default {
  name: 'Form',
  data() {
    return {
      persona: {
        nombre: '',
        email: '',
        pass: '',
        fechaNacimiento: '',
        edad: null
      }
    };
  },
  watch: {
    'persona.fechaNacimiento'(nuevaFecha) {
      this.persona.edad = this.calcularEdad(nuevaFecha);
    }
  },
  methods: {
    guardarDatos() {
      const edad = this.calcularEdad(this.persona.fechaNacimiento);
      this.persona.edad = edad;

      
      alert(
        `Usuario creado correctamente\n` +
        `Nombre: ${this.persona.nombre}\n` +
        `Email: ${this.persona.email}\n` +
        `Contraseña: ${this.persona.pass}\n` +
        `Fecha de nacimiento: ${this.persona.fechaNacimiento}\n` +
        `Edad: ${this.persona.edad} años`
      );

    
      this.limpiarFormulario();
    },

    calcularEdad(fechaNac) {
      const fechaNacimiento = new Date(fechaNac);
      const hoy = new Date();
      let edad = hoy.getFullYear() - fechaNacimiento.getFullYear();
      const mes = hoy.getMonth() - fechaNacimiento.getMonth();

      if (mes < 0 || (mes === 0 && hoy.getDate() < fechaNacimiento.getDate())) {
        edad--;
      }
      return edad;
    },

    limpiarFormulario() {
      
      this.persona.nombre = '';
      this.persona.email = '';
      this.persona.pass = '';
      this.persona.fechaNacimiento = '';
      this.persona.edad = null;
    }
  }
};
</script>

<template>
    <form @submit.prevent="guardarDatos">
        <input type="text" placeholder="Nombre de usuario" v-model="persona.nombre"><br>
        <input type="mail" placeholder="Email" v-model="persona.email"><br>
        <input type="password" placeholder="Constraseña" v-model="persona.pass"><br>
        <input type="date" v-model="persona.fechaNacimiento"><br>
        <button type="submit">Enviar</button>
    </form>

    <div v-if="persona.nombre || persona.email || persona.pass || persona.fechaNacimiento || persona.edad">
        <h3>Datos del Usuario</h3>
        <p>Nombre: {{ persona.nombre }}</p>
        <p>Email: {{ persona.email }}</p>
        <p>Contraseña: {{ persona.pass }}</p>
        <p>Fecha de Nacimiento: {{ persona.fechaNacimiento }}</p>
        <p>Edad: {{ persona.edad }}</p>
    </div>
</template>


<style>

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
