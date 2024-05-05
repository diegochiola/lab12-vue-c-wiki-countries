<script setup>
import { defineProps } from "vue";


const props = defineProps({ countries: Array });
</script>

<template>
  <section class="flex">
    <ul>
      <li v-for="(country, index) in countries" :key="index" class="card">
        <RouterLink :to="`/list/${country.alpha3Code}`" class="router-link">
          <img
            :src="`https://flagcdn.com/20x15/${country.alpha2Code.toLowerCase()}.png`"
            alt=""
            class="flag-icon"
          />
          {{ country.name.common }}
        </RouterLink>
      </li>
    </ul>
    <router-view></router-view>
  </section>
</template>

<style scoped>
.flex {
  padding: 40px;
  display: flex;
  justify-content: space-around;
}
.card {
  display: flex;
  align-items: center;
  width: 500px;
 padding: 30px;
}
li {
  list-style: none;
  cursor: pointer;
  
}
li:hover {
  background-color: #f5f5f5;
}
.router-link {
  text-decoration: none;
}
</style>
