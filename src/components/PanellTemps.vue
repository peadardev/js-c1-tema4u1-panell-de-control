<template>
  <section class="card">
    <h3>Temps a {{ lloc }}</h3>
    <div v-if="temperatura">
      <div class="clima">
        <span>{{ clima }}</span>
        <img :src="icona" class="icona-clima" />
        <em>(Observació: {{ actualitzat }})</em>
      </div>
      <p>Temp: {{ temperatura }}°C · HR: {{ humitat }}% · Vent: {{ vent }} Km/h</p>
    </div>
    <div v-else>No disponible...</div>
  </section>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
const lloc = ref<string>('Barcelona');
const clima = ref<string>('');
const icona = ref<string>('');
const temperatura = ref<string>('');
const humitat = ref<string>('');
const vent = ref<string>('');
const actualitzat = ref<string>('');

async function obtenirTemps() {
  const resposta = await fetch(`https://wttr.in/${lloc.value}?format=j1`);
  return await resposta.json();
}

onMounted(async () => {
  const dades = await obtenirTemps();
  clima.value = dades.current_condition[0].lang_ca[0].value;
  icona.value = dades.current_condition[0].weatherIconUrl[0].value;
  temperatura.value = dades.current_condition[0].temp_C;
  humitat.value = dades.current_condition[0].humidity;
  vent.value = dades.current_condition[0].windspeedKmph;
  actualitzat.value = dades.current_condition[0].observation_time;
});
</script>

<style scoped>
.card {
  background: lightcyan;
}
.clima {
  display: flex;
  align-items: center;
  gap: 1rem;
}
.icona-clima {
  width: 24px;
  height: auto;
}
</style>
