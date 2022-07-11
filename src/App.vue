<template>
  <div class="container">
    <!-- App Header -->
    <TheHeader />
    <main 
      class="text-center" v-if="!state.loading">
      <!-- Title Section -->
      <TheTitle :title="state.title" :dataDate="state.dataDate"/>
      <!-- Data Section -->
      <DataDisplay :data="state.stats"/>
      <!-- Country Selector -->
      <CountrySelect @countryChange="getCountryData" :countries="state.countries"/>
      <!-- Boton para limpiar busqueda -->
      <button
      @click="clearContrySelection"
      v-if="state.stats.Country" 
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
        Limpiar Búsqueda
      </button>
    </main>
    <!-- Vista de carga de datos -->
    <main 
      class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Recolectando Datos 📥
    </div>
    <img 
      src="./assets/loading.gif" 
      alt="Loading Image"
      class="w-24 m-auto">
    </main>
  </div>
</template>
<script setup>
import TheHeader from "./components/TheHeader.vue";
import TheTitle from "./components/TheTitle.vue"
import DataDisplay from "./components/DataDisplay.vue";
import CountrySelect from "./components/CountrySelect.vue";
// App State
import loadingImage from "./assets/loading.gif";
import { reactive } from "vue";

let state = reactive({
  loading: true,
  title: "Global",
  dataDate: "",
  stats: {},
  countries: [],
});
// Metodo para la recolección de datos
async function fetchCovidData() {
  const res = await fetch("https://api.covid19api.com/summary");
  const data = await res.json();
  return data;
}
// Metodo para el cambio de pais
function getCountryData(country) {
  // Se actualizan las estadisticas a mostrar 
  state.stats = country
  // Se actualiza el titulo
  state.title = country.Country;
}

function updateData(summary) {
  state.dataDate = summary.Date;
  state.stats = summary.Global;
  state.countries = summary.Countries;
  state.loading = false;
}

// Limpiando Selección
const clearContrySelection = async () => {
  state.loading = true;
  state.title = "Global 🌍"
  const covidSummary = await fetchCovidData();
  updateData(covidSummary);
}

// Rutina de inicialización
(async () => {
  const covidSummary = await fetchCovidData();
  updateData(covidSummary);
})();
</script>