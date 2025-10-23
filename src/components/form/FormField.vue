<script setup lang="ts">
import SelectField, { type SelectFieldProps } from '@/components/form/SelectField.vue'
import { computed } from 'vue'
import type { TextFieldProps } from './TextField.vue'
import TextField from './TextField.vue'
import MultiCheckField, { type MultiCheckFieldProps } from './MultiCheckField.vue'
import TextareaField, { type TextareaProps } from './TextareaField.vue'
export type FieldType = 'select' | 'text' | 'email' | 'multiCheck' | 'textarea'

export type SharedInputProps = {
  name: string
  label?: string
  type: FieldType
  placeholder?: string
  required?: boolean
  id?: string
  error?: ((fieldName: string) => string) | string
}

type Props = SharedInputProps &
  (SelectFieldProps | TextFieldProps | MultiCheckFieldProps | TextareaProps)

const {
  label: intrinsicLabel,
  error: intrinsicError,
  placeholder: intrinsicPlaceholder,
  ...props
} = defineProps<Props>()

const error =
  intrinsicError === undefined
    ? 'this is a validation Error'
    : typeof intrinsicError === 'string'
      ? intrinsicError
      : intrinsicError(props.name)
const label = (intrinsicLabel ?? props.name) + (props.required ? '*' : '')
const placeholder = intrinsicPlaceholder ?? 'TYPE HERE'

const fieldMap = {
  select: SelectField,
  text: TextField,
  email: TextField,
  multiCheck: MultiCheckField,
  textarea: TextareaField,
} as const
const FieldComponent = fieldMap[props.type]
</script>

<template>
  <div class="field" v-bind="$attrs">
    <label :for="name">{{ label }}<span class="requiredText">: required</span></label>
    <component
      :class="['input', props.type === 'multiCheck' && 'without-border']"
      :is="FieldComponent"
      v-bind="props"
      :placeholder="placeholder"
    />
    <div class="error">{{ error }}</div>
  </div>
</template>

<style scoped>
.field {
  position: relative;
  padding-bottom: 24px;
  text-transform: uppercase;
}

label {
  display: block;
  font-size: 0.75rem;
  color: var(--color-secondary);
  display: block;
}
.input {
  --field-h-padding: 16px;
  --field-v-padding: 15px;

  margin-top: 8px;
  border: 1px solid var(--color-cream);
  border-radius: 8px;
  padding: var(--field-v-padding) var(--field-h-padding);
  box-sizing: border-box;
}

.input:is(:focus, :active) {
  outline: 2px solid var(--color-cream);
  outline-offset: -1px;
}

.error {
  display: none;
}

.input:has(:user-valid) {
  border-color: var(--color-accent);
}

.input:has(:user-invalid),
.input:is(:user-invalid) {
  border-color: var(--color-red);
}

.input:has(:user-valid),
.input:is(:user-valid) {
  border-color: var(--color-accent);
}

:is(.input:has(:user-invalid), .input:is(:user-invalid)) + .error {
  position: absolute;
  bottom: 5.5px /* try to convert with calc considering font-size with rem */;
  display: block;
  color: var(--color-red);
  font-size: 0.625rem;
}

.requiredText {
  display: none;
}
.field:has(:placeholder-shown:user-invalid) .requiredText,
.field:has(.multi-check input:first-of-type[required]:user-invalid) .requiredText {
  display: inline;
}

.input.without-border {
  border: none;
  outline: none;
  padding: 0px;
}
</style>
