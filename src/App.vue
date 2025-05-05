<script setup>
import Header from "./components/Header.vue";
import Card from "./components/Card.vue";
import {ref} from "vue";

const score = ref(0)

const cards = ref([
  {
    id: 1,
    state: 'closed',
    status: 'pending',
    word: 'Alex',
    translation: 'Алексей'
  },
  {
    id: 2,
    state: 'closed',
    status: 'pending',
    word: 'Hockey',
    translation: 'Хоккей'
  },
  {
    id: 3,
    state: 'closed',
    status: 'pending',
    word: 'The Dog',
    translation: 'Собака'
  }
]);

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
            v-for="card in cards" :key="card.id"
            v-bind='card'
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
