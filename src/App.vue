<script setup>
//@ts-check
import { computed, ref, watch } from "vue";
import porfile from "./components/porfile.vue";
import favorites from './components/favorites.vue';
import FooterChris from'./components/v-footer-ch19.vue';
// breakpoint de los telefonos se esta usando por defecto 600px 
const phoneBreakPoint = 600;
const widthActual = ref(window.innerWidth);
const imagenGithub = 'data:image/png;base64,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'
window.addEventListener('resize', ()=>{
  widthActual.value = window.innerWidth;
})
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
          const itsExistence = favoritesList.value.get(user.value);
          console.log(itsExistence);
          if(!!itsExistence){
            userData.value = itsExistence;
          }else{
          const response = await fetch(API + user.value);
            const data = await response.json();
            // console.log(data);
            // variable para capturar objetos con los datos del usuario buscando en la api de github
            userData.value = data
            console.log(userData);
            user.value = '';
          }
        }
</script>

<template>
<div class="bigContainer">
  <!-- <h1>{{ widthActual }}</h1> -->
  <favorites v-if="widthActual > phoneBreakPoint" class="favorites" :user-string="user" :favs="favoritesList" @favorite-selected="selectedfav"></favorites>
  <div class="form-container">
    <h3 style="display: flex;">{{saludo}} <img height="32" width="32" src="https://cdn.jsdelivr.net/npm/simple-icons@v9/icons/github.svg" /></h3>
   <div>
    <!-- buscador  -->
    <input type="text" placeholder="introduce a github name or user" v-model="user">
    <!-- boton para buscar los usuarios en github  -->
    <button class="sendButton" v-on:click.prevent="doSearch">Send</button>
  </div>
  <porfile :data-user="userData" @favorites-data="cambiarValor"></porfile>
  <favorites v-if="widthActual < phoneBreakPoint" class="favorites" :user-string="user" :favs="favoritesList" @favorite-selected="selectedfav"></favorites>
    <hr/>
    </div>
    <FooterChris></FooterChris>
</div>
</template>

<style scoped>
  .sendButton{
    cursor: pointer;
  }
</style>
