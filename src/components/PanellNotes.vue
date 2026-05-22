<template>
  <section class="card">
    <h3>Notes</h3>
    <span class="intro-nota">
      <input
        class="text-note-field"
        v-model="textNota"
        type="text"
        minlength="1"
        maxlength="40"
        placeholder="(introduiu text; màxim 40 càracters)"
      />
      <button @click="createNote">Acceptar</button>
    </span>
    <div>{{ textNota.length }}/40</div>
    <span class="linea-nota" v-for="note of llistaNotes" :key="note.id">
      <div class="note-text">{{ note.text }}</div>
      <span class="date-and-button">
        <div class="note-date">{{ note.date }}</div>
        <button class="boto-elimina" @click="deleteNote(note.id)">Elimina</button>
      </span>
    </span>
    <div>
      <p>Total notes: {{ llistaNotes.length }}</p>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const textNota = ref<string>('');
export interface Note {
  id: number;
  text: string;
  date: string;
}
const llistaNotes = ref<Note[]>([]);

function createNote() {
  if (!textNota.value) {
    window.alert('El text no pot estar buit');
    return;
  }
  const newNote: Note = {
    id: nextId(),
    text: textNota.value,
    date: new Date().toLocaleString('ca-ES'),
  };
  llistaNotes.value.push(newNote);
  textNota.value = '';
}

function nextId() {
  const ids: number[] = llistaNotes.value.map((note) => note.id);
  if (ids.length === 0) return 0;
  return Math.max(...ids) + 1;
}

function deleteNote(noteId: number) {
  llistaNotes.value = llistaNotes.value.filter((note) => note.id !== noteId);
}
</script>

<style scoped>
.card {
  background: lightgreen;
}
.intro-nota {
  display: flex;
  gap: 2px;
}
.text-note-field {
  width: 460px;
  height: 24px;
}
.linea-nota {
  display: flex;
  align-items: center;
  justify-content: space-between;
  vertical-align: center;
  background: lightyellow;
  border-radius: 5px;
  padding: 4px;
  margin: 2px;
}
.note-text {
  display: flex;
  font-size: 12px;
  font-weight: bold;
}
.date-and-button {
  align-items: center;
  display: flex;
}
.note-date {
  display: flex;
  font-size: 12px;
  font-style: italic;
  padding-right: 5px;
}
button {
  gap: 16px;
  background-color: green;
  color: white;
  border: none;
  padding: 12;
  border-radius: 5px;
  font-size: 12px;
  cursor: pointer;
}
.boto-elimina {
  background-color: red;
  height: 1.5rem;
}
</style>
