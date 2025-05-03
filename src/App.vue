<script setup>
import Button from "./components/Button.vue";
import Header from "./components/Header.vue";
import Cards from "./components/Cards.vue";

function showTranslate() {
  console.log("showTranslate from emit")
}
function changeStatus(value) {
  console.log("changeStatus emit with value = ", value)
}
</script>

<template>
  <Header />
  <Cards @show-translate="showTranslate" @change-status="changeStatus" />
  <Button>Начать игру</Button>
</template>

<style scoped>

</style>
