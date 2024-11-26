<script setup>
console.log("Has cargado 'CountryView.vue'")
import { ref,watch } from 'vue'
import { useRoute } from 'vue-router'
import ExperienceComponent from '../components/ExperienceComponent.vue'
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
    <article>
      <img class="imagenPrincipal" :src="pathImagenes+country.image" :alt="'Imagen de '+ country.image">
      <p class="descripcion">{{ country.description }}</p>
    </article>
  </section>

  <section>
    <h1>Experiences on {{ country.name }}</h1>
    <ExperienceComponent v-for="(experiencia, index) in country.experiences" :key="index"
      :experiencia="experiencia"
      :id="index"
    />
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
</style>

