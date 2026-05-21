<template>
  <section class="card">
    <h3>Temps</h3>
    <p v-if="temperatura">
      {{ clima }} · Temp: {{ temperatura }}°C · HR: {{ humitat }}% · Vent: {{ vent }} Km/h
    </p>
    <p v-else>Carregant...</p>
  </section>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
const temperatura = ref<string>('');
const humitat = ref<string>('');
const vent = ref<string>('');
const clima = ref<string>('');

async function obtenirTemps() {
  const resposta = await fetch('https://wttr.in/Barcelona?format=j1');
  return await resposta.json();
}

onMounted(async () => {
  const dades = await obtenirTemps();
  temperatura.value = dades.current_condition[0].temp_C;
  humitat.value = dades.current_condition[0].humidity;
  vent.value = dades.current_condition[0].windspeedKmph;
  clima.value = dades.current_condition[0].lang_ca[0].value;
});
</script>

<style scoped>
.card {
  background: lightcyan;
}
</style>
