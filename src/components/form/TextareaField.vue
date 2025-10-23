<script setup lang="ts">
import type { SharedInputProps } from './FormField.vue'

export type TextareaProps = {
  type: 'textarea'
}
type Props = SharedInputProps & TextareaProps

const props = defineProps<Props>()
</script>

<template>
  <textarea v-bind="props" rows="7" type="textfield" />
</template>

<style scoped>
textarea {
  /* all: unset; */
  color: var(--color-cream);
  background: var(--bg-primary);
  text-transform: none;
  box-sizing: border-box;
  width: 100%;
  font-family: var(--font-secondary);
  font-weight: 700;
  text-align: start;
  vertical-align: text-top;
}
</style>
