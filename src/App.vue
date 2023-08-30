<script setup>
import { ref } from "vue";
import porfile from "./components/porfile.vue";

const API = "https://api.github.com/users/";
const saludo = 'Hola mundo'
// se utiliza la variable user para obtener data de los inputs para los usuarios 
const user = ref(null);
let userData = ref(null);
// funcion y metodo para cargar los usuarios de github 
async function doSearch() {
    // consulta al api de github mas el nombre del usuario 
            const response = await fetch(API + user.value);
            const data = await response.json();
            console.log(data);
            // variable para capturar objetos con los datos del usuario buscando en la api de github
            userData.value = data
            console.log(userData);
            user.value = '';
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
    <porfile :data-user="userData"></porfile>
    <hr>
    </div>
</div>
</template>

<style scoped>


</style>
