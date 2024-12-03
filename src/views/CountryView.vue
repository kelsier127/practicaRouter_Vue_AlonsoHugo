<script setup>
console.log("Has cargado 'CountryView.vue'")
import { ref,watch } from 'vue'
import { useRoute } from 'vue-router'
import data from '@/assets/data.json';

let pathImagenes = '../src/assets/images/';

const route = useRoute()

const id = ref(route.params.id - 1)

let country = data.destinations[id.value]

console.log(data.destinations[id.value])
console.log(route.params.id)

watch(
  () => route.params.id,
  (newId) => {
    id.value = newId - 1
    country = data.destinations[id.value]
    console.log(data.destinations[id.value])
  }
)

</script>

<template>
  <section>
    <h1>{{ country.name }}</h1>
    <h1> Este es el route: {{ route.params.id }}</h1>
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

  <section>
    <RouterView/>
  </section>
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

