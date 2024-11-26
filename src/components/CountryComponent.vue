<script setup>
const props = defineProps({
  country:Object
})

let pais = props.country

console.log(pais)
</script>

<template>
  <div class="paisComponent">
    <h2>{{ country.name }}</h2>
    <img :src="'../src/assets/images/'+country.image" alt="">
  </div>
</template>

<style scoped>
.paisComponent{
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  border-radius: 10px;
  width: 35%;
  padding: 20px;
  margin: 15px;
  box-shadow: 2px 2px 4px 2px;
  border: 2px solid black;
  background-color: rgb(212, 212, 212);
}

img{
  border-radius: 12px;
  border: 2px solid black;
}

</style>

