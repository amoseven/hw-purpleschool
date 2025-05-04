<script setup>
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";
import {ref} from "vue";

const score = ref(0)
// const state = ref(false);
// const status = ref('pending');
// const translation = ref('Алексей')
// const word = ref('Alex')

const cards = ref([
  {
    state: false,
    status: 'pending',
    word: 'Alex',
    translation: 'Алексей'
  }
]);

function showTranslate(newValue) {
  state.value = newValue
}

function changeStatus(value) {
  console.log("changeStatus emit with value = ", value)
}
</script>

<template>
  <main>
    <Header :scores="score"/>
    <Cards
        v-bind='cards[0]'
        @show-translate="showTranslate"
        @change-status="changeStatus"/>
  </main>
</template>
