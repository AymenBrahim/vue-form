<script setup lang="ts">
import { ref } from 'vue'
import type { SharedInputProps } from './FormField.vue'

type Option = { label: string; value: string }
export type MultiCheckFieldProps = { options: Option[] }
type Props = SharedInputProps & MultiCheckFieldProps

const { options, required, name, id } = defineProps<Props>()
const isChecked = ref<number>(0)

function toggleInput(position: number) {
  const checked = getInputIsChecked(position)
  if (!checked) {
    isChecked.value |= 1 << position // set bit
  } else {
    isChecked.value &= ~(1 << position) // clear bit
  }
}

function getInputIsChecked(position: number) {
  return ((isChecked.value >> position) & 1) === 1
}
</script>

<template>
  <fieldset :id class="multi-check">
    <input
      tabindex="-1"
      v-if="required && isChecked === 0"
      required
      type="checkbox"
      class="required"
    />

    <label v-for="(option, i) in options" :key="option.value">
      <span>{{ option.label }}</span>
      <input
        :name
        :value="option.value"
        :checked="getInputIsChecked(i)"
        @input="toggleInput(i)"
        type="checkbox"
      />
    </label>
  </fieldset>
</template>

<style scoped>
fieldset {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

label {
  font-family: var(--font-secondary);
  font-weight: 700;
  font-size: 1rem;
  color: var(--color-cream);

  padding: 15px 16px;
  border: 1px solid var(--color-cream);
  border-radius: 24px;

  cursor: pointer;
  transition:
    color 70ms ease-in-out,
    border 70ms ease-in-out;
}

label:hover,
label:has(input:checked) {
  color: var(--color-accent);

  border: 1px solid var(--color-accent);

  transition:
    color 0.2s ease-in-out,
    border 0.2s ease-in-out;
}

label:has(input:is(:focus, :active)) {
  outline: 2px solid var(--color-cream);
  outline-offset: -1px;
}

input {
  all: unset;
  position: absolute;
  width: 0;
  height: 0;
}
</style>
