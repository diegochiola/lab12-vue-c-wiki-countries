<script setup>
import Navbar from './components/Navbar.vue'
import { ref } from 'vue'

const countries = ref(null);

async function fetchCountries(){
  const response = await fetch('https://ih-countries-api.herokuapp.com/countries')
  const finalResponse = await response.json();

  countries.value = finalResponse;
}
fetchCountries()

</script>

<template>
  <div class="app">
    <Navbar/>
    <router-view :countries="countries"/>

  </div>
</template>

<style scoped></style>
