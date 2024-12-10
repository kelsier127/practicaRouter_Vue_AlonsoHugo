<script setup>
console.log("Has cargado 'CountryView.vue'")
import { useRoute,useRouter } from 'vue-router'
import data from '@/assets/data.json';
import { computed } from 'vue';

let pathImagenes = '/images/';

const route = useRoute()
const router = useRouter()

const props = defineProps({
  id: String
})


let country = computed(()=> {
  let destination;
  for(let i in data.destinations){
    if(data.destinations[i].id == props.id){
      destination = data.destinations[i]
    }
  }
  return destination
} )



const goBack = ()=>{
  console.log(route.fullPath)
  if(route.fullPath.includes('experience')){
    router.push(`/country/${country.value.id}`);
  }else{
    router.push(`/`);
  }
}

</script>

<template>
  <section>
    <h1>{{ country.name }}</h1>
    <button @click="goBack"> Go back </button>
    <article>
      <img class="imagenPrincipal" :src="pathImagenes+country.image" :alt="'Imagen de '+ country.image">
      <p class="descripcion">{{ country.description }}</p>
    </article>
  </section>

  <section>
    <h1>Experiences on {{ country.name }}</h1>
    <div class="experiences">
      <RouterLink v-for="(experience,index) in country.experiences" :key="experience" :to="'/country/'+country.id+'/experience/'+index">
        <div class="experienceContainer">
          <p>{{ experience.name }}</p>
          <img :src="pathImagenes+experience.image" alt="">
        </div>
      </RouterLink>
    </div>
  </section>

  <div>
    <RouterView/>
  </div>
</template>

<style>
section{
  border-radius: 10px;
  box-shadow: 2px 2px 3px 2px;
  margin:2% 10%;
  padding: 3%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: rgb(212, 212, 212);
}
article{
  display: flex;
  justify-content: center;
  align-items: center;
}

button{
  width: 100px;
  margin: 15px;
}
.descripcion{
  padding-left: 60px;
}
.imagenPrincipal{
  border-radius: 10px;
  border: 2px solid black;
}

img{
  border-radius: 10px;
}

.experienceContainer{
  display: flex;
  align-items: center;
  flex-direction: column;
  border: 1px solid gray;
  background-color: rgb(153, 153, 153);
  padding: 15px;
  border-radius: 8px;
}

.experiences{
  display: flex;
  justify-content: space-around;
}
</style>

