<script setup lang="ts">
type ButtonProps = {
  primary?: boolean
  secondary?: boolean
  withTransition?: boolean
  small?: boolean
}
const { secondary, withTransition = true, small = false } = defineProps<ButtonProps>()
</script>

<template>
  <button
    role="button"
    :class="[secondary && 'secondary', withTransition && 'with-transition ', small && 'small']"
    v-bind="$attrs"
  >
    <slot></slot>
  </button>
</template>

<style scoped>
button {
  pointer-events: all;
  display: block;
  cursor: pointer;
  box-sizing: border-box;
  font-family: var(--font-secondary);
  text-align: center;
  text-transform: uppercase;
  color: var(--color-accent);

  background: var(--bg-primary);

  width: 100%;
  padding: 15px 16px;

  border: 1px solid var(--color-accent);
  border-radius: 8px;
}

button.small {
  padding: 4px 8px;
  width: fit-content;
}

button {
  transition:
    color 0.3s var(--animation-ease-out-expo),
    background-color 0.3s var(--animation-ease-out-expo);
}

button:hover {
  background: var(--color-accent);
  color: var(--bg-primary);
  border: 1px solid var(--color-accent);
}

button:is(:focus, :active) {
  outline: 2px solid hsl(from var(--color-accent) h s 30%);
  outline-offset: -1px;
  background: var(--color-accent);
  color: var(--bg-primary);
  border: 1px solid var(--color-accent);
}
</style>
