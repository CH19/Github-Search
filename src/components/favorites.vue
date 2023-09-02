<script setup>
//@ts-check
import { onMounted } from "vue";

const props = defineProps({
    // con la prop favs se importan los favoritos del componnente Porfile, esto se hace tambien comunicando un emmit al componente padre 
    favs: {
        type: Map,
        required: true,
        default: null,
    }
});
onMounted(()=>{
    console.log('favoritos montados');
})
// onUpdated(()=>{
//     props.favs.forEach((element, value) => {
//     console.warn(`${JSON.stringify(element.login)}: ${value}`);
// });
// })
</script>
<template>
    <div class="favorites">
        <!-- aqui se puede usar el metodo favs.values() para cargar en el arreglo solo los valores pero me interesa tener el key del map 
        para usarlo como key del for  -->
            <div class="favorite" v-for="fav in favs" :key="fav[0]">
                <a class="favorite__link" :href="fav[1].html_url" target="_blank">
                    <img :src="fav[1].avatar_url" :alt="fav[1].name" class="favorite__avatar">
                    <span class="favorite__name">{{ fav[1].login }}</span>
                </a>
            </div>
        </div>
</template>

<style scoped>
@import url(../css/variables.css);
@import url(../../node_modules/bootstrap/dist/css/bootstrap-utilities.rtl.css) all;

    .favorites {
  position: fixed;
  top: 0;
  left: 0;
  width: fit-content;
  display: grid;
  grid-template-columns: repeat(3, 90px);
  gap: 10px;
}

.favorite {
    background: var(--naranja5);
  transition: transform 0.3s ease-out;
  border-radius: 20px;
  width:fit-content;
  height: fit;
}
.favorite__name{
    color: var(--white);
}
.favorite__link{
    text-decoration: none;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    
}

.favorite__avatar {
  height: 5rem;
  width: 5rem;
    border-radius: 20px;
  margin: 0.3rem;
}

.favorite--selected {
  transform: scale(1.3);
}

/* Transitions */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
  position: absolute;
}
</style>