<script setup>
import TheHeader from "./components/TheHeader.vue";
// App State
import loadingImage from "./assets/loading.gif";
import { reactive } from "vue";
console.log(loadingImage);

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
(async () => {
  const covidSummary = await fetchCovidData();
  state.dataDate = covidSummary.Date;
  state.stats = covidSummary.Global;
  state.countries = covidSummary.countries;
  state.loading = false;
})();
</script>

<template>
  <!-- App Header -->
  <TheHeader />
  <main 
    class="text-center" v-if="!state.loading">
    Show Data
  </main>
  <main 
    class="flex flex-col align-center justify-center text-center" v-else>
  <div class="text-gray-500 text-3xl mt-10 mb-6">
    Fetching Data
  </div>
  <img 
    src="./assets/loading.gif" 
    alt="Loading Image"
    class="w-24 m-auto">
  </main>
</template>
