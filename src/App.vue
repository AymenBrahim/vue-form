<script setup lang="ts">
import HeaderComponent from './components/HeaderComponent.vue'
</script>

<template>
  <HeaderComponent />
  <main>
    <div style="background-color: #fff; min-height: 100vh; width: 100vw"></div>
  </main>
</template>
<style>
iframe {
  height: calc(100vh - var(--header-height));
  width: 100%;
}
</style>
