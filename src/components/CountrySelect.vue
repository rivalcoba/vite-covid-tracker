<template>
  <select
    @change="updateSelection"
    v-model="selected"
    class="form-select mt-10 block w-full border p-3 rounded"
  >
    <!-- Selección por defecto -->
    <option value="0">Seleccionar País</option>
    <option v-for="country in countries" :value="country.ID" :key="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script setup>
// Importando funcion de referencia reactiva
// emisión de eventos
import { ref, defineEmits } from "vue";
// Propiedades
const props = defineProps(["countries"]);
// State Selected in zero by default
const selected = ref(0);
// Emisión de eventos
const emit = defineEmits(['countryChange']);
// Metodo
const updateSelection = () => {
  // Buscando de la lista de paises aquel cuyo Id
  // coincida con el seleccionado
  const selectedCountry = props.countries.find((country) => {
    return country.ID === selected.value;
  });
  emit('countryChange', selectedCountry);
}
</script>