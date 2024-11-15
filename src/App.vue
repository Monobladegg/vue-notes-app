<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);

function randomHsl() {
  return "hsla(" + Math.random() * 360 + ", 100%, 50%, 0.5)";
}

const addNote = () => {
  if (newNote.value === "") {
    return;
  }
  notes.value.push({
    text: newNote.value,
    date: new Date(),
    id: notes.value.length,
    backgroundColor: randomHsl(),
  });
  newNote.value = "";
  showModal.value = false;
};

const toggleModal = (condition) => {
  showModal.value = condition;
};
</script>

<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
        <p style="color: black">{{ notes }}</p>
        <textarea
          v-model="newNote"
          name="note"
          id="note"
          cols="30"
          rows="10"
        ></textarea>
        <button class="add" @click="addNote()">Add note</button>
        <button class="close" @click="toggleModal(false)">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="toggleModal(true)">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" :style="{ backgroundColor: note.backgroundColor }" class="card">
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
  /* align-items: center; */
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: #0a7e8c;
}

button {
  border: none;
  border-radius: 50%;
  color: white;
  padding: 10px;
  width: 50px;
  height: 50px;
  background-color: #0a7e8c;
  cursor: pointer;
}

.card {
  width: 225px;
  height: 225px;
  background-color: #0a7e8c;
  padding: 10px;
  border-radius: 10px;
  margin-right: 20px;
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.date {
  text-align: left;
  font-weight: bold;
  font-size: 12px;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  height: 100vh;
  width: 100vw;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background-color: white;
  width: 750px;
  height: 500px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  padding: 50px;
}

.modal button {
  padding: 10px 20px;
  width: 100%;
  background-color: blueviolet;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 20px;
  margin-top: 15px;
}

.modal .close {
  background-color: red;
}

textarea {
  width: 100%;
  height: 75%;
  border: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.9);
  border-radius: 16px;
  padding: 10px;
  font-size: 20px;
}
</style>
