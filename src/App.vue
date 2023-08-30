<script setup>
import { ref } from "vue";

const API = "https://api.github.com/users/";
const saludo = 'Hola mundo'
// se utiliza la variable user para obtener data de los inputs para los usuarios 
const user = ref('');
// funcion y metodo para cargar los usuarios de github 
async function doSearch() {
            const response = await fetch(API + user.value);
            const data = await response.json();
            console.log(data);
            alert('solicitud llegada');
          }
</script>

<template>
<div class="bigContainer">
  <div class="form-container">
    <h3>{{saludo}}</h3>
   <div>
    <!-- buscador  -->
    <input type="text" placeholder="introduce a user" v-model="user">
    <!-- boton para buscar los usuarios en github  -->
    <button v-on:click="doSearch">Send</button>
    </div>
    <hr>
    </div>
</div>
</template>

<style scoped>


</style>
