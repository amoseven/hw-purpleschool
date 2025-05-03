<script setup>
import Heart from "./icons/Heart.vue";

const { scores } = defineProps({
  'scores': {
    type: Number,
    default: 100
  }
})
</script>

<template>
<div class="score">
  <p class="value">{{scores}}</p>
  <Heart />
</div>
</template>

<style scoped>
.score {
  background: var(--color-secondary);
  border-radius: 36px;
  display: flex;
  flex-direction: row;
  justify-content: center;
/*  align-items: flex-start;*/
  align-items: center;
  padding: 12px 24px;
  gap: 10px;
  width: 110px;
  height: 48px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.15);
}

.value {
  font-family: var(--font-family);
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
  text-align: center;

}
</style>
