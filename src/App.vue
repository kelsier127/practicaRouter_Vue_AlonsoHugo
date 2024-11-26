<script setup>

import { RouterLink, RouterView } from 'vue-router'
import data from '@/assets/data.json';

let countryData = data;

console.log(countryData)

</script>

<template>
  <header>
    <nav id="nav">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink v-for="(country,index) in countryData.destinations" :key="index" :to="'../country/'+country.id"> {{ country.name }} </RouterLink>
    </nav>
  </header>

  <RouterView/>
</template>

<style scoped>
.nav-menu{
  margin: 0;
  display: flex;
  justify-content: space-around;
  background-color: aqua;
}
</style>
