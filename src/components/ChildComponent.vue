<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg?: string }>();

const nombre = ref("")
const email = ref("")
const password = ref("")
const fechaNac = ref("")


const calcularEdad = () => {
  if (!fechaNac.value) return null;
  const hoy = new Date();
  const nacimiento = new Date(fechaNac.value);
  const mes = hoy.getMonth() - nacimiento.getMonth();
  let edad = hoy.getFullYear() - nacimiento.getFullYear();
  if (mes < 0 || (mes === 0 && hoy.getDate() < nacimiento.getDate())) {
    edad--;
  }
  return edad;
};

function handleForm (){
    if (nombre.value && email.value && password.value && fechaNac.value){
        if (nombre.value.length > 3){
            let usuario = {
                nombre: nombre.value,
                email: email.value,
                password: password.value,
                fechaNac: fechaNac.value

            }
            console.log(usuario)
            nombre.value = ""
            email.value = ""
            password.value = ""
            fechaNac.value = ""

    alert(`Usuario registrado correctamente: Nombre: ${usuario.nombre} Email: ${usuario.email} Fecha de nacimiento: ${usuario.fechaNac}`);

        }
        
        else { alert("El nombre de usuario debe tener más de 3 carateres")}
    }
    else { alert("Debe completar los campos")}
    

}

</script>

<template>
    <h2> {{ msg }}</h2>
    <form @submit.prevent="handleForm">
        <input type="text" placeholder="Nombre de Usuario" v-model="nombre">
        <input type="email" placeholder="Email" v-model="email">
        <input type="password" placeholder="Contraseña" v-model="password">
        <input type="date" placeholder="Fecha de Nacimiento" v-model="fechaNac">
        <input type="submit" value="enviar">
    </form>
    <div class="preview">
      <h3>Vista previa:</h3>
      <p><strong>Nombre:</strong> {{ nombre }}</p>
      <p><strong>Email:</strong> {{ email }}</p>
      <p v-if="fechaNac"><strong>Edad:</strong> {{ calcularEdad() }} años</p>
    </div>
</template>


<style scoped>
form {
  max-width: 400px;
  margin: 20px auto;
  padding: 15px;
  background-color: #99c5c7;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

form input[type="text"],
form input[type="email"],
form input[type="password"],
form input[type="date"],
form input[type="submit"] {
  display: block;
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

form input[type="submit"] {
  background-color: #51657a;
  color: white;
  font-weight: bold;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

form input[type="submit"]:hover {
  background-color: #36475a;
}

h2 {
  text-align: center;
  color: #343a40;
  font-family: Arial, sans-serif;
  margin-bottom: 20px;
}

.preview {
  max-width: 400px;
  margin: 20px auto;
  padding: 15px;
  background-color: #cbb6e4;
  border: 1px solid #ffeeba;
  border-radius: 8px;
}

.preview h3 {
  margin-bottom: 10px; /* Espaciado con los datos */
  margin-top: -10px; /* Reduce el espacio superior */
  color: #353149;
}


.preview p {
  margin: 5px 0;
  color: #664370;
}


</style> 