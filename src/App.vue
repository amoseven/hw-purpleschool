<script setup>
import Button from "./components/Button.vue";
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";

function showTranslate(lang) {
  console.log("showTranslate from emit with Lang = ", lang)
}
function changeStatus(value) {
  console.log("changeStatus emit with value = ", value)
}
</script>

<template>
  <main>
    <Header />
    <Cards @show-translate="showTranslate" @change-status="changeStatus" />
    <Button>Начать игру</Button>
  </main>
</template>
