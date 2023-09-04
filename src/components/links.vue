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
             <a class="links-ancla text-decoration-none" :href="ch19Data.dataUser?.html_url">
               <button class="links-button">
                 <figure>
                   <svg
                     xmlns="http://www.w3.org/2000/svg"
                     width="16"
                     height="16"
                     fill="currentColor"
                     class="bi bi-github"
                     viewBox="0 0 16 16"
                   >
                     <path
                       d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.012 8.012 0 0 0 16 8c0-4.42-3.58-8-8-8z"
                     />
                   </svg>
                 </figure>
                 <span>Github</span>
               </button>
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
    align-items: center;
}
.links-button figure{
    height: fit-content;
    width: fit-content;
}
</style>