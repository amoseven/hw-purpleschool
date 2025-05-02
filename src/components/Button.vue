<script setup>

</script>

<template>
<button class="button">
  <slot></slot>
</button>
</template>

<style scoped>
.button {
  font-family: var(--font-family);
  width: 335px;
  height: 68px;
  border-radius: 100px;
  padding: 16px 10px;
  line-height: 36px;
  font-size: 24px;
  color: var(--color-card);
  background: var(--color-primary);
  border: none;
}
</style>
