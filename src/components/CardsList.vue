<script setup>
import Card from "./Card.vue";

const {cards} = defineProps({
  cards: {
    type: Array,
    default: () => []
  }
})

const emit = defineEmits(['open-card', 'change-status'])

</script>

<template>
  <div class="cards-list">
    <Card
        v-for="card in cards"
        :key="card.id"
        v-bind='card'
        :id="card.id"
        @open-card="payload => emit('open-card', payload)"
        @change-status="payload => emit('change-status', payload)"

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
