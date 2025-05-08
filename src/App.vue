<script setup>
import {onMounted, ref} from "vue";
import Header from "./components/Header.vue";
import CardsList from "./components/CardsList.vue";

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

function openCard(id) {
  const card = cards.value.find(card => card?.id === id);
  if (card) {
    card.state = 'opened'
  }
}

function changeStatus({id, status}) {
  const card = cards.value.find(card => card?.id === id);
  if (card) {
    card.status = status;
    const multiple = (status === 'success') ? 1 : -1;
    score.value += multiple * 100;

  }
}

onMounted(() => {
  load()
})


</script>

<template>
  <Header :scores="score"/>

  <main>
    <CardsList :cards="cards"
               @open-card="openCard"
               @change-status="changeStatus"/>
  </main>

</template>
