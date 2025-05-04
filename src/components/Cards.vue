<script setup>

import {computed } from "vue";

import Ok from "./icons/Ок.vue"
import Cancel from "./icons/Cancel.vue"

const emit = defineEmits(['show-translate', 'change-status'])
const { state, translation, word, status } = defineProps({
  status: {
    type: String,
    default: 'pending'
  },
  state: {
    type: Boolean,
    default: false
  },
  word: {
    type: String,
    default: "Перевод"
  },
  translation: {
    type: String,
    default: "Перевод"
  },
})

const word_on_card = computed(() => state ? translation : word);

const text_action = computed(() => status !== 'pending' ? 'Завершено' : 'Перевернуть');
const isPending = computed(() => status === 'pending' && state);



function showTranslate() {
  emit('show-translate', !state)
}

function changeStatus(value) {
  emit('change-status', value)
}
</script>

<template>
  <div class="card-wrap">
    <div class="card-inner">
      <p class="card-caption">{{ word_on_card }}</p>

      <p v-if="!isPending" class="card-action" @click="showTranslate()">{{ text_action }}</p>

      <div class="card-status" v-else>
        <Cancel :size="24" @click="changeStatus(0)"/>
        <Ok :size="24" @click="changeStatus(1)"/>
      </div>

        <Cancel v-if="status==='fail'" :size="32" class="card-result" />
        <Ok v-if="status==='success'" :size="32" class="card-result" />

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

  .card-result {
    position: absolute;
    top: -14px;
  }


}
</style>
