<script setup>
import Card from "./Card.vue";

const {cards} = defineProps({
  cards: {
    type: Array,
    default: () => []
  }
})

const emit = defineEmits(['set-score'])

function openCard(id) {
  const card = cards.find(card => card.id === id);
  if(card) {
    card.state = 'opened'
  }
}

function changeStatus({id, status}) {
  const card = cards.find(card => card.id === id);
  if(card) {
    card.status = status;
    const multiple = (status === 'success') ? 1 : -1;
    emit('set-score', multiple*100);
  }
}
</script>

<template>
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
</template>

<style scoped>
.cards-list {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  gap: 25px;
}
</style>
