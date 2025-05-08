<script setup>

import {computed} from "vue";

import Ok from "./icons/Ок.vue"
import Cancel from "./icons/Cancel.vue"

const emit = defineEmits(['open-card', 'change-status'])
const {id, state, translation, word, status} = defineProps({
  id: {
    type: Number,
    required: true
  },
  status: {
    type: String,
    default: 'pending'
  },
  state: {
    type: String,
    default: 'closed'
  },
  word: {
    type: String,
    default: "English"
  },
  translation: {
    type: String,
    default: "Английский"
  },
})

const isOpen = computed(() => state === 'opened')
const isPending = computed(() => status === 'pending' && isOpen.value);

const word_on_card = computed(() => isOpen.value ? translation : word);
const text_action = computed(() => isOpen.value ? 'Завершено' : 'Перевернуть');

function openCard() {
  emit('open-card', id)
}

function changeStatus(value) {
  emit('change-status', {id, status: value})
}
</script>

<template>
  <div>
    <div class="card-wrap">
      <div class="card-inner">

        <p class="card-caption">{{ word_on_card }}</p>

        <p v-if="!isPending" class="card-action" @click="openCard()">{{ text_action }}</p>

        <div v-if="isPending" class="card-status">
          <Cancel :size="24" @click="changeStatus('fail')"/>
          <Ok :size="24" @click="changeStatus('success')"/>
        </div>

        <div v-if="!isPending">
          <Cancel v-if="status==='fail'" :size="32" class="card-result"/>
          <Ok v-if="status==='success'" :size="32" class="card-result"/>
        </div>

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
