<script setup>
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";
import {ref} from "vue";

const isFlipped = ref(false);
const scores = ref(55)
const wordRus = ref('Алексей')
const wordEng = ref('Alex')

function showTranslate(newValue) {
  isFlipped.value = newValue
}
function changeStatus(value) {
  console.log("changeStatus emit with value = ", value)
}
</script>

<template>
  <main>
    <Header :scores="scores" />
    <Cards
        :is-flipped="isFlipped"
        :word-rus="wordRus"
        :word-eng="wordEng"
        @show-translate="showTranslate"
        @change-status="changeStatus" />
  </main>
</template>
