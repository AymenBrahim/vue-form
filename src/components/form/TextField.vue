<script setup lang="ts">
import type { SharedInputProps } from './FormField.vue'

export type TextFieldProps = {
  type: 'text' | 'email'
}
type Props = SharedInputProps & TextFieldProps

const props = defineProps<Props>()
</script>

<template>
  <input v-bind="props" />
</template>

<style scoped>
input {
  all: unset;
  box-sizing: border-box;
  width: 100%;
  font-family: var(--font-secondary);
  font-weight: 700;
}
</style>
