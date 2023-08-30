<script setup>
import { computed, onMounted, reactive, ref } from "vue";

// objeto con los parametros a solicitar 
onMounted(()=>{
    console.log('componente montado ');
})
const counter = ref(0);
const keyMap = ref(0);
const moreCounter = computed(()=>{
    if(counter.value > 10)
        return 'Hola';
    else 
        return ' adios';
})
const props = defineProps({
        dataUser: {
            type: Object,
            required: true,
        },

    })
    const favorites = ref(new Map());
    const itsfavorite = computed(()=>{
      if(props.dataUser.id){
        return favorites.value.has(props.dataUser.id.toString()) ? true: false;
      }else
        return 'Np hay datos';
    })
    
    function addFavorite(key){
        favorites.value.set(key?.id.toString(), key);
        console.log(favorites.value.get(key?.id));
    }
    function removeFavorite(key){
        favorites.value.delete(key?.id);
        console.log(favorites.value.size);
    }
</script>

<template>
        <div class="porfile-container">
            <button @click="counter++">{{ counter }}: {{ moreCounter }}</button>
            <div class="porfile" v-if="dataUser != null && dataUser?.login">
                <div>
                    <a href="#" v-if="!itsfavorite" class="porfile__toggle-favorite" @click="addFavorite(dataUser)">Add Favorite ⭐️ {{ itsfavorite }} {{ dataUser.id}}</a>
                <a href="#" v-else class="porfile__toggle-favorite" @click="removeFavorite(dataUser)">Remove fvorite ⭐️</a>
                </div>

                <h2 class="porfile__name">{{ dataUser?.login }}</h2>
                <img :src="dataUser?.avatar_url" alt="" class="porfile__avatar">
                <p class="porfile__bio">{{ dataUser?.location }}
                    <br>
                    <a :href="dataUser?.html_url" class="porfile__blog">{{ dataUser?.html_url }}</a>
                </p>
            </div>
            <div class="porfile__error" v-else>Error found</div>
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