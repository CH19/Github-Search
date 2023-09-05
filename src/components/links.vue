<script setup>
import { onBeforeMount, ref } from 'vue';
const API = "https://api.github.com/users/";
const user = 'ch19';
let ch19Data = ref('');
async function ch19Loaded() {
         fetch(API + user)
         .then(response => {
            if(response.ok) return response.json();
         }).then(json => ch19Data.value = json).catch(error => console.error(error));
          }
onBeforeMount(()=>{
    console.log('ch19 component');
    ch19Loaded();
})
</script>

<template>
  <div class="links-container">
    <article :v-if="ch19Data.length > 1 " class="loguito" id="Ig-Caption">
      <span>Make By CH19</span>
            <figure>
              <img :src="ch19Data.avatar_url" alt="">
              </figure>
              <a class="links-ancla links-button text-decoration-none" :href="ch19Data.dataUser?.html_url">
                <img height="32" width="32" src="https://cdn.jsdelivr.net/npm/simple-icons@v9/icons/github.svg"/>
                <span>Github</span>
              </a>
            </article>

    </div>

</template>

<style scoped>
.links-container{
    height: 3rem;
    display: flex;
    
}
.loguito{
    display: flex;
    flex-direction: row ;
    justify-content: space-around;
    align-items: center;
}
figure{
    width: 5rem;
    height: 5rem;
}
figure img{
    object-fit: contain;
    width: 100%;
    height: 100%;
    border-radius: 50%;
}
.links-button{
    cursor: pointer;
    background: linear-gradient(to bottom, #24292e, #ffffff);
    display: flex;
    width: fit-content;
    height: fit-content;
    padding: 10px;
    border-radius: 6px;
    align-items: center;
}
.links-button figure{
    height: fit-content;
    width: fit-content;
}
.links-button span {
  color: #fff;
}
</style>