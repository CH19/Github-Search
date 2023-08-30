<script setup>
// @ts-check
// importaciones de los metodos y propiedades de vue 
import { computed, onMounted, reactive, ref, watch } from "vue";

// objeto con los parametros a solicitar 
// Metodo para saber si el componente esta montado 
onMounted(()=>{
    console.log('componente montado ');
})
// propiedades del usuario transferidos por el padre 
const props = defineProps({
        dataUser: {
            type: Object,
            required: true,
        },

    })
    // mapa con la lista de usuarios favoritos a buscar 
    const favorites = reactive(new Map());
    // propiedad para saber si el usuario tiene un favorito y que espera para que retorne 
    const itsfavorite = computed(()=>{
    //    validacion otra vez de que la propiedad con el id no este vacia 
        if(props.dataUser.id){
            return favorites.has(props.dataUser.id.toString()) ? true: false;
      }else
      return 'No hay datos';
    })
    // funcion para annadir un favorito en donde se pide como unico paramatreo de key la data para el id del map y la informacion del usuario 
    function addFavorite(key){
        // console.log(key);
       if(key != undefined || key != null){
        favorites.set(key?.id.toString(), key);
        console.log(favorites.get(key.id.toString()));

        favorites.forEach((value, key) => {
            console.log(`${key} ${JSON.stringify(value)}`);
        })
       }else{
        console.log('no definido');
       }
    }
    // funcion para remover el favorito
    function removeFavorite(key){
        // recordar colocar el metodo toString en todas las llamadas 
        favorites.delete(key?.id.toString());
        console.log(favorites);
}
</script>

<template>
        <div class="porfile-container">
            <div class="porfile" v-if="dataUser != null && dataUser?.login">
                <div>
                    <!-- div con la informacion de annadir o quitar favoritos  -->
                    <a href="#" v-if="!itsfavorite" class="porfile__toggle-favorite" @click="addFavorite(props.dataUser)">Add Favorite ⭐️</a>
                <a href="#" v-else class="porfile__toggle-favorite" @click="removeFavorite(dataUser)">Remove favorite ⭐️</a>
                </div>

                <h2 class="porfile__name">{{ dataUser?.login }}</h2>
                <img :src="dataUser?.avatar_url" alt="" class="porfile__avatar">
                <p class="porfile__bio">{{ dataUser?.location }}
                    <br>
                    <a :href="dataUser?.html_url" class="porfile__blog">{{ dataUser?.html_url }}</a>
                </p>
            </div>
            <div class="porfile__error" v-if="dataUser != null && !(dataUser?.login)">Error found</div>
        </div>

</template>

<style scoped>
@import url(../css/variables.css);
.porfile-container{
    padding: 20px;
    margin: 10px;
}
    .porfile {
  position: relative;
  background-color: var(--naranja5);
  border-radius: 0.3rem;
  box-shadow: 2px 2px 3px var(--naranja4);
  color: var(--white);;
  padding: 2.5rem;
  display: grid;
  gap: 1rem;
  grid-template-areas:
    "name name"
    "avatar bio";
}

.porfile__toggle-favorite {
  position: absolute;
  top: 0.3rem;
  right: 0.3rem;
  border: none;
  color: var(--white);
  text-decoration: none;
  padding: 0.4rem;
  font-size: 1.2rem;
}
.porfile__toggle-favorite:hover{
    color: var(--naranj2);
}

.porfile__name {
  grid-area: name;
  margin: 0.4rem 0;
}

.porfile__avatar {
  grid-area: avatar;
  max-width: 6rem;
  height: auto;
  border-radius: 1rem;
}

.porfile__bio {
  grid-area: bio;
  margin: 0;
}

.porfile__blog {
  grid-area: blog;
  color: goldenrod;
}

.porfile__error {
  padding: 0.3rem;
  background-color: tomato;
  color: var(--white);;
  text-align: center;
  border: 1px solid red;
}
</style>

