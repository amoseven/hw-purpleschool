<script setup>
import {onMounted, ref} from "vue";
import Header from "./components/Header.vue";
import CardsList from "./components/CardsList.vue";
import Button from "./components/Button.vue";

const isStartScreen = ref(true)
const score = ref(0)
const cards = ref([]);

const API_BASE = "http://localhost:8080/api";
const API_PATH = "/random-words";

async function load() {
  const urlApi = `${API_BASE}${API_PATH}`;
  try {
    const rs = await fetch(urlApi);
    const data = await rs.json();

    cards.value = data.map((item, i) => {
      return {
        id: i + 1,
        state: 'closed',
        status: 'pending',
        word: item.word,
        translation: item.translation
      }
    })

  } catch (e) {
    console.log(e)
  }
}

async function startGame() {
  isStartScreen.value = false;
  await load();
}

async function restartGame() {
  score.value = 0;
  await load();
}

function openCard(id) {
  const card = cards.value.find(card => card?.id === id);
  if (card) {
    card.state = 'opened'
  }
}

function calculateScores(status) {
  const bonus = (status === 'success') ? 10 : -4;
  score.value += bonus;
}

function changeStatus({id, status}) {
  const card = cards.value.find(card => card?.id === id);
  if (card) {
    card.status = status;
    calculateScores(status)

  }
}

onMounted(() => {
  load()
})


</script>

<template>
  <Header :scores="score"/>

  <main class="main-block">
    <Button v-if="isStartScreen" @click="startGame()">Начать</Button>
    <div v-else>
      <CardsList
          :cards="cards"
          @open-card="openCard"
          @change-status="changeStatus"
      />

      <Button @click="restartGame()">Начать заново</Button>
    </div>
  </main>

</template>

<style>
.main-block {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
}
</style>
