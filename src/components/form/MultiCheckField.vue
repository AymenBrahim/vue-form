<script setup lang="ts">
import { computed, ref } from 'vue'
import type { SharedInputProps } from './FormField.vue'

type Option = { label: string; value: string }
export type MultiCheckFieldProps = { options: Option[] }
type Props = SharedInputProps & MultiCheckFieldProps

const { options, required, name, id } = defineProps<Props>()
// reactive boolean array, one per option
const isChecked = ref<boolean[]>(Array.from({ length: options.length }, () => false))

const onClick = (e: PointerEvent) => {
  e.preventDefault()
  e.stopPropagation()
  e.stopImmediatePropagation()

  const currentTarget = e.currentTarget as HTMLElement
  const input = currentTarget.nextElementSibling as HTMLInputElement
  const index = options.findIndex((v) => v.value === input.value)
  console.log(isChecked.value.toString())
  console.log(index)
  if (index < 0) return
  isChecked.value[index] = !isChecked.value[index]
  input.click()
}

const isEmpty = computed(() => !isChecked.value.some((checked) => checked))
</script>

<template>
  <fieldset :id class="multi-check">
    <input tabindex="-1" v-if="required && isEmpty" required type="checkbox" class="required" />

    <label v-for="option in options" :key="option.value">
      <span @click="onClick($event)">{{ option.label }}</span>
      <input :name :value="option.value" type="checkbox" />
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
  outline: 1px solid var(--color-cream);
}

input {
  position: absolute;
  left: -200vw;
}
</style>
