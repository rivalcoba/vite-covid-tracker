<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- BOX 1 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">
        Casos
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nuevos:</span>
        {{ NewConfirmed }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Totales:</span>
        {{ TotalConfirmed }}
      </div>
    </div>
    <!-- BOX 2 -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">
        Fallecimientos
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nuevos:</span>
        {{ NewNewDeaths }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Totales:</span>
        {{ TotalDeaths }}
      </div>
    </div>
  </div>
</template>

<script setup>
// Importando Computed
import { computed } from "vue";
// Definiendo Propiedad de entrada
const props = defineProps(['data']);
// Number separator
const numberWithCommas = (number) => number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
// Computed Properties
const NewConfirmed = computed(()=>numberWithCommas(props.data.NewConfirmed));
const TotalConfirmed = computed(()=>numberWithCommas(props.data.TotalConfirmed));
const NewNewDeaths = computed(()=>numberWithCommas(props.data.NewDeaths));
const TotalDeaths = computed(()=>numberWithCommas(props.data.TotalDeaths));
</script>