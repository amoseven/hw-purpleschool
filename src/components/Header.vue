<script setup>
import Score from "./Score.vue";
import {ref} from "vue";

const scores = ref(100)
</script>

<template>
<div class="app-header">
<p class="app-name">Запомни слово</p>
  <Score :scores="scores" />
</div>
</template>

<style scoped>
.app-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 1440px;
  height: 121px;

}
.app-name {
  color: var(--color-card-inverted);
  text-transform: uppercase;
  font-family: var(--font-family);
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;

}
</style>
