<script setup lang="ts">
import DrawerComponent from './DrawerComponent.vue'
</script>

<template>
  <header><span>studio freight</span> <DrawerComponent /></header>
</template>

<style scoped>
header {
  position: sticky;
  display: flex;

  padding: 0 24px;
  height: var(--header-height);
  align-items: center;
}
header > span {
  font-family: var(--font-secondary);
  text-transform: uppercase;
  font-size: 1.5rem;
}
</style>
