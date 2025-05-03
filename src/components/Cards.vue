<script setup>

import {ref} from "vue";
import Ok from "./icons/Ок.vue"
import Cancel from "./icons/Cancel.vue"

const text_action = ref('Перевернуть')
const {text_rus, text_eng = 'translate'} = defineProps(['text_rus', 'text_eng'])
const emit = defineEmits(['show-translate', 'change-status'])

function showTranslate() {
  emit('show-translate')
}

function changeStatus(value) {
  emit('change-status', value)
}
</script>

<template>
  <div class="card-wrap">
    <div class="card-inner">
      <p class="card-caption">{{ text_eng }}</p>
      <p class="card-action" @click="showTranslate">{{ text_action }}</p>
      <div class="card-status">
        <Cancel :size="24" @click="changeStatus(0)"/>
        <Ok :size="24" @click="changeStatus(1)"/>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-wrap {
  background: var(--color-card);
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  padding: 19px;
  width: 250px;
  height: 376px;
}

.card-inner {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100%;
  border-radius: 12px;
  border-width: 1px;
  border-style: solid;
  border-color: var(--color-secondary);
}

.card-inner {
  position: relative;

  .card-caption {
    color: var(--color-card-inverted);
    font-weight: 400;
    font-size: 18px;
    line-height: 100%;
    text-align: center;
  }

  .card-action {
    position: absolute;
    bottom: -20px;
    color: var(--color-card-inverted);
    text-transform: uppercase;
    padding: 0 4px;
    background: var(--color-card);
    font-weight: 700;
    font-size: 12px;
    line-height: 18px;
    display: none;
  }

  .card-status {
    position: absolute;
    bottom: -15px;
    padding: 5px 15px;
    background: var(--color-card);
    display: flex;
    justify-content: space-between;
    gap: 48px;
  }


}
</style>
