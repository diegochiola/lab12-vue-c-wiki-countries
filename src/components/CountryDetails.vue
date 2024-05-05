<script setup>
import { ref, computed, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const country = ref(null);

const countryCode = computed(() => {
  return route.params.alpha3Code;
});

const getCountryByAlphaCode = async () => {
  const alpha3Code = route.params.alpha3Code;

  const response = await fetch(
    `https://ih-countries-api.herokuapp.com/countries/${alpha3Code}`
  );

  const finalResponse = await response.json();

  country.value = finalResponse;
};
getCountryByAlphaCode();

watch(countryCode, (newCountryCode) => {
  getCountryByAlphaCode();
});

const flagUrl = computed(() => {
  if (country.value) {
    const alpha2Code = country.value.alpha2Code.toLowerCase();
    return `https://flagcdn.com/72x54/${alpha2Code}.png`;
  } else {
    return "";
  }
});
</script>

<template>
  <section v-if="country">
    <img :src="flagUrl" :alt="`Flag of ${country.name.common}`" />
    <h1>{{ country.name.common }}</h1>
  </section>
</template>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
h1 {
  color: blue;
}
</style>
