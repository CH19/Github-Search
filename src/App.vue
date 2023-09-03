<script setup>
//@ts-check
import { ref, watch } from "vue";
import porfile from "./components/porfile.vue";
import favorites from './components/favorites.vue'
window.localStorage.setItem('cosita', 'Mi nombre es christian');

const API = "https://api.github.com/users/";
const saludo = ref( 'Github Search')
// se utiliza la variable user para obtener data de los inputs para los usuarios 
const user = ref('');
let userData = ref(null);
let favoritesList = ref(new Map());
// funcion para obtener los favorites del componente favorites 
function cambiarValor(msj){

 return  favoritesList.value = msj;
}
function selectedfav(name){
  user.value = name
  doSearch()
}
// funcion y metodo para cargar los usuarios de github 
async function doSearch() {
    // consulta al api de github mas el nombre del usuario 
            const response = await fetch(API + user.value);
            const data = await response.json();
            // console.log(data);
            // variable para capturar objetos con los datos del usuario buscando en la api de github
            userData.value = data
            console.log(userData);
          }
</script>

<template>
<div class="bigContainer">
  <favorites class="favorites" :favs="favoritesList" @favorite-selected="selectedfav"></favorites>
  <div class="form-container">
    <h3>{{saludo}}</h3>
   <div>
    <!-- buscador  -->
    <input type="text" placeholder="introduce a user" v-model="user">
    <!-- boton para buscar los usuarios en github  -->
    <button class="sendButton" v-on:click="doSearch">Send</button>
  </div>
    <porfile :data-user="userData" @favorites-data="cambiarValor"></porfile>
    <hr>
    </div>
</div>
</template>

<style scoped>
  .sendButton{
    cursor: pointer;
  }
</style>
