<script setup>
import data from '@/assets/data.json';
import { ref,watch } from 'vue'
import { useRoute } from 'vue-router';



const route = useRoute()

const id = ref(route.params.id - 1)

let country = data.destinations[id.value]

const expId = ref(route.params.expId)

let experience = country.experiences[expId.value]

watch(
  () => route.params.id,
  (newId) => {
    id.value = newId - 1
    country = data.destinations[id.value]
    console.log(data.destinations[id.value])
  }
)
let pathImagenes = ref(`/images/${experience.image}`);

watch(
  () => route.params.expId,
  (newId) => {
    expId.value = newId
    experience = country.experiences[expId.value]
    pathImagenes.value= `/images/${experience.image}`
    console.log(experience)
    console.log(pathImagenes.value)
  }
)


</script>

<template>
  <div class="experienceContainer">
    <h1>{{ experience.name }}</h1>
    <div class="experienceContainerTotal">
      <img :src="pathImagenes" alt="">
      <p class="experienceDescription">
        {{ experience.description }}
      </p>
    </div>

  </div>
</template>

<style scoped>
.experienceContainerTotal{
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: justify;
  text-justify: inter-word;
}

.experienceDescription{
  padding: 40px;
}

.experienceContainer{
  border-radius: 10px;
  box-shadow: 2px 2px 3px 2px;
  margin:2% 10%;
  padding: 3%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background-color: rgb(212, 212, 212);
}
</style>
