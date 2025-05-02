<script setup>

</script>

<template>
<button class="button">
  <slot></slot>
</button>
</template>

<style scoped>
.button {
  font-family: var(--font);
  width: 335px;
  height: 68px;
  border-radius: 100px;
  padding: 16px 10px;
  line-height: 36px;
  font-size: 24px;
  color: var(--color-primary);
  background: var(--color-bg-main);
  border: none;
}
</style>
