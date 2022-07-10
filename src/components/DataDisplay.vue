<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">
        Casos
      </h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">Nuevos:</span>
        {{ data.NewConfirmed }}
      </div>
    </div>
  </div>
</template>

<script setup>
// Definiendo Propiedad de entrada
const props = defineProps(['data']);
</script>