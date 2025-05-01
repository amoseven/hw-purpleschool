<script setup>
import {computed} from "vue";

function formatDate(date) {

  let dd = date.getDate().toString().padStart(2, '0');
  let mm = (date.getMonth() + 1).toString().padStart(2, '0')
  let yy = date.getFullYear()

  let hh = date.getHours().toString().padStart(2, '0')
  let ii = date.getMinutes().toString().padStart(2, '0')
  let ss = date.getSeconds().toString().padStart(2, '0')

  return `${dd}.${mm}.${yy} ${hh}:${ii}:${ss}`;
}

const currentFullDate = computed(() => formatDate(new Date()))

</script>

<template>
  <h1>{{ currentFullDate }}</h1>
</template>

<style scoped>

</style>
