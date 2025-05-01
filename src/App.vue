<script setup>
function formatDate(date) {

  let dd = date.getDate();
  if (dd < 10) dd = '0' + dd;

  let mm = date.getMonth() + 1;
  if (mm < 10) mm = '0' + mm;

  let yy = date.getFullYear()

  return dd + '.' + mm + '.' + yy;
}

const currentDate = formatDate(new Date());
</script>

<template>
  <h1>{{ currentDate}}</h1>
</template>

<style scoped>

</style>
