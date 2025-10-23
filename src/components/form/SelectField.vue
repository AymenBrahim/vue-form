<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import type { SharedInputProps } from './FormField.vue'

export interface Option {
  label: string
  value: string
}
/*
export type SelectFieldProps = {
  name: string
  modelValue: string | number | null
  options: Option[]
  placeholder?: string
  required?: boolean
} */

export type SelectFieldProps = {
  type: 'select'
  options: Option[]
}
type Props = SharedInputProps & SelectFieldProps
const props = defineProps<Props>()

const isOpen = ref(false)
const selectedOption = ref({ value: '', label: '' })
const toggleOpen = () => (isOpen.value = !isOpen.value)
const close = () => (isOpen.value = false)
const select = (option: Option) => {
  selectedOption.value = option
  close()
}
const onClickOutside = (e: MouseEvent) => {
  const target = e.target as HTMLElement
  if (!target.closest('.container')) close()
}

onMounted(() => document.addEventListener('click', onClickOutside))
onBeforeUnmount(() => document.removeEventListener('click', onClickOutside))

console.log(!!selectedOption?.value)
</script>

<template>
  <div
    v-bind="$attrs"
    :class="['container', isOpen && 'is-open', !!selectedOption?.value && 'is-selected']"
    :style="`--total-length:${props.options.length * 33.1}px;`"
    role="combobox"
  >
    <!-- Trigger -->
    <button
      type="button"
      @click="toggleOpen"
      role="button"
      :aria-expanded="isOpen"
      tabindex="0"
      :aria-owns="name + 'list'"
    >
      <span>{{
        (selectedOption && selectedOption.label) || (placeholder ?? 'Choose an option')
      }}</span>
      <svg
        class="chevron"
        width="16"
        height="14"
        viewBox="0 0 16 14"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        aria-hidden
      >
        <path d="M7.79419 0L15.5884 13.5L-3.91006e-05 13.5L7.79419 0Z" fill="currentColor" />
      </svg>
    </button>
    <transition name="fade">
      <ul v-if="isOpen" :id="`${name}-listbox`" role="listbox">
        <li
          v-for="option in options"
          :key="option.value"
          :class="{ selected: option.value === selectedOption.value }"
          @click="select(option)"
          role="option"
          :aria-selected="false"
        >
          {{ option.label }}
        </li>
      </ul>
    </transition>
    <select
      :id="name + 'list'"
      :name="props.name"
      :required="props.required"
      aria-hidden
      tabindex="-1"
    >
      <option value="" selected disabled></option>
      <option
        v-for="option in options"
        :selected="option.value === selectedOption.value"
        :key="option.value"
        :value="option.value"
      >
        {{ option.label }}
      </option>
    </select>
    <!-- Dropdown -->
  </div>
</template>

<style scoped>
select {
  all: unset;
  /* visibility: none; */
  bottom: 0;
  position: absolute;
  width: 0;
}

.container {
  --transition-time: 75ms;

  position: relative;
  cursor: pointer;
  font-family: var(--font-secondary);
  font-weight: 700;
}

.container:has(button:focus) {
  outline: 2px solid var(--color-cream);
  outline-offset: -1px;
}

button {
  all: unset;
  display: flex;
  justify-content: space-between;

  width: 100%;
}

button::after {
  content: '';
  position: absolute;
  inset: 0;
  border-radius: 8px;
}

.container:not(.is-selected) button span {
  color: var(--color-secondary);
}

button .chevron {
  width: 18px;
  height: 18px;
  margin-top: -1px;

  transition: transform 0.2s ease;
}

ul {
  position: absolute;
  top: calc(100% - var(--field-v-padding));
  background: var(--bg-primary);
  border-radius: 8px;
  border: 1px solid var(--color-cream);
  border-top: 0;
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;

  width: 100%;
  padding: 0;
  padding-top: var(--field-v-padding);

  margin: 0;
  margin-left: calc(var(--field-h-padding) * -1 - 1px);

  z-index: var(--z-pop-over);
  overflow: hidden;
  list-style-type: none;
}

.container:has(button:is(:focus, :active)) ul {
  border: 2px solid var(--color-cream);
  border-top: none;
  width: 100%;
  margin-left: calc(var(--field-h-padding) * -1 - 2px);
}

li {
  padding: 7px 0 6px var(--field-h-padding);
  position: relative;
}

li:last-child {
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
}

li.selected,
li:hover {
  background: var(--color-cream);
  color: var(--bg-primary);
}

ul:has(li:not(.selected):hover) li.selected {
  background: var(--bg-primary);
  color: var(--color-cream);
}

.container.is-open li.selected {
  outline: 1px dashed var(--color-cream);
  outline-offset: -1px;
}

.container.is-open {
  padding-bottom: 0px;
}
.container.is-open button {
  padding-bottom: 15px;
}
.container.is-open button .chevron {
  transform: rotateZ(180deg);
}

.fade-enter-active,
.fade-leave-active {
  transition: max-height 0.75s var(--animation-ease-out-expo);
  max-height: var(
    --total-length
  ); /* this should be calculated with rem for font size and not only with pxs */
}
.fade-enter-from,
.fade-leave-to {
  transition: max-height 0.75s var(--animation-ease-out-expo);
  max-height: 0px;
}

@media (prefers-reduced-motion: reduce) {
  .fade-enter-active,
  .fade-leave-active {
    transition: none; /* this should be calculated with rem for font size and not only with pxs */
  }
  .fade-enter-from,
  .fade-leave-to {
    transition: none;
  }
}
</style>
