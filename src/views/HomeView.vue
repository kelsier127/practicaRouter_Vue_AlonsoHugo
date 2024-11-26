<script setup>
import data from '@/assets/data.json';
import CountryComponent from '../components/CountryComponent.vue'

let countryData = data;

console.log(countryData)
</script>

<template>
  <main>
    <div class="muestraPaises">
      <CountryComponent v-for="(country, index) in countryData.destinations" :key="index"
        :country="country"
      />
    </div>
  </main>
</template>

<style scoped>
.muestraPaises{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
