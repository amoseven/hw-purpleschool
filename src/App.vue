<script setup>
import Header from "./components/Header.vue";
import Card from "./components/Card.vue";
import {onMounted, ref} from "vue";

const score = ref(0)
const cards = ref([]);

const API_BASE = "http://localhost:8080/api";
const API_PATH = "/random-words";

async function load() {
  const urlApi = `${API_BASE}${API_PATH}`;
  try {
    const rs = await fetch(urlApi);
    const data = await rs.json();
    console.log(data)

    cards.value = data.map((item, i) => {
      return {
        id: i+1,
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

onMounted(() => {
  load()
})

function openCard(id) {
  const card = cards.value.find(card => card.id === id);
  if(card) {
    card.state = 'opened'
  }
}

function changeStatus({id, status}) {
  const card = cards.value.find(card => card.id === id);
  if(card) {
    card.status = status;
    const multiple = (status === 'success') ? 1 : -1;
    score.value += multiple*100;
  }
}
</script>

<template>
  <Header :scores="score"/>

  <main>
    <div class="cards-list">
      <Card
          v-for="card in cards"
          :key="card.id"
          v-bind='card'
          :id="card.id"
          @open-card="openCard"
          @change-status="changeStatus"

      />
    </div>

  </main>

</template>

<style scoped>
.cards-list {
  display: flex;
  flex-wrap: wrap;
  gap: 25px
}
</style>
