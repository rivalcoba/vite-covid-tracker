<template>
  <div class="text-center">
    <h2 class="text-3xl font-bold">{{ title }}</h2>
    <div class="text-2xl mt-4 mb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script setup>
// Importando momentJs
import moment from "moment";
// Importando prop
import { computed } from "vue";
// Definiendo Propiedades
const props = defineProps(["title", "dataDate"]);
// Creando propiedades
const timestamp = computed(() =>
  moment(props.dataDate).format("MMMM DD YYYY, hh:mm:ss a")
);
</script>