<script setup>
import { ref } from "vue";

let countries = ref(null);

async function obtainData() {
  try {
    const response = await fetch("https://ih-countries-api.herokuapp.com/countries");
    if (!response.ok) throw new Error("Error al obtener los datos");
    const jsonResponse = await response.json();
    jsonResponse.sort((a, b) => {
      // Comparar los nombres en minúsculas para evitar problemas de mayúsculas
      return a.name.common.localeCompare(b.name.common);
    });
    countries.value = jsonResponse;
    return jsonResponse;
  } catch (err) {
    console.error("Something went wrong!", err);
  }
}
obtainData();

</script>

<template>
  <div class="containerCountriesList">
    <ul v-if="countries">
      <li v-for="(country, index) in countries" :key="index" class="country-item">
        <router-link :to="`/list/${country.alpha3Code}`" class="country-link">
          <img :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`" 
            alt="Bandera de {{ alphaCodeCountries.name.common }}"
            class="flag"/> 
          <span class="country-name">{{ country.name.common }}</span>
        </router-link>
      </li>
    </ul>
  </div>
  <router-view></router-view>
</template>

<style scoped>
.containerCountriesList {
  display: flex;
  flex-direction: column;
  height: 80%;
  overflow-y: auto;
  width: 20%;
  border: 1px solid #ccc;
  padding: 0;
}

.containerCountriesList::-webkit-scrollbar {
  width: 12px;
}

.containerCountriesList::-webkit-scrollbar-track {
  background: #f1f1f1;
}

.containerCountriesList::-webkit-scrollbar-thumb {
  background-color: #888;
  border-radius: 10px;
  border: 2px solid #f1f1f1;
  height: 30px;
}

.containerCountriesList::-webkit-scrollbar-thumb:hover {
  background-color: #555;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.country-item {
  width: 100%;
  height: 150px;
  display: flex;
  align-items: center;
  padding: 10px 5px;
  padding: 10px;
  transition: background-color 0.3s ease;
  border-bottom: 1px solid #e0e0e0;
}

.country-item:hover {
  background-color: #f0f0f0;
}

.country-link {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-decoration: none;
  color: #333;
  width: 100%;
}

.flag {
  width: 32px;
  height: auto;
  object-fit: cover;
}

.country-name {
  font-size: 16px;
  color: #1976d2;
}
</style>