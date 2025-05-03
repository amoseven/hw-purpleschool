<script setup>
// import Button from "./components/Button.vue";
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";
import {ref} from "vue";

const isFlipped = ref(false);

function showTranslate(newValue) {
  isFlipped.value = newValue
}
function changeStatus(value) {
  console.log("changeStatus emit with value = ", value)
}
</script>

<template>
  <main>
    <Header />
    <Cards
        :is-flipped="isFlipped"
        word="The Cat"
        @show-translate="showTranslate"
        @change-status="changeStatus" />
<!--    <Button>Начать игру</Button>-->
  </main>
</template>
