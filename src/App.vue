<script setup>
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";
import {ref} from "vue";

const state = ref(false);
const status = ref('pending');
const scores = ref(55)
const translation = ref('Алексей')
const word = ref('Alex')

function showTranslate(newValue) {
  state.value = newValue
}
function changeStatus(value) {
  console.log("changeStatus emit with value = ", value)
}
</script>

<template>
  <main>
    <Header :scores="scores" />
    <Cards
        :status="status"
        :state="state"
        :translation="translation"
        :word="word"
        @show-translate="showTranslate"
        @change-status="changeStatus" />
  </main>
</template>
