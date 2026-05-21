<script setup lang="ts">
import PanellHora from './components/PanellHora.vue'
import PanellTemps from './components/PanellTemps.vue'
import PanellNotes from './components/PanellNotes.vue'
</script>

<template>
  <div class="panel">
    <h1>Panell de control</h1>
    <PanellHora />
    <PanellTemps />
    <PanellNotes />
  </div>
</template>

<style>
body {
  font-family: Arial, sans-serif;
}
.panel {
  padding: 0.5rem;
  background: darkblue;
  color: white;
  border: 2px solid black;
  border-radius: 0.5rem;
  text-align: center;
}
.card {
  padding: 2rem;
  margin: 1px;
  background: lightyellow;
  color: black;
  border: 1px solid lightgray;
  border-radius: 0.5rem;
  text-align: left;
}
</style>
