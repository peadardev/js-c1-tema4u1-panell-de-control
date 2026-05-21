<template>
  <section class="card">
    <h3>Hora</h3>
    <p>{{ hora }}</p>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const hora = ref<string>(new Date().toLocaleTimeString('ca-ES'));
setInterval(() => {
  hora.value = new Date().toLocaleTimeString();
}, 1000);
</script>

<style scoped>
.card {
  background: lightyellow;
}
</style>
